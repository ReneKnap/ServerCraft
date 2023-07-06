## UseCase
Es sollte möglich sein Datein von bestimmten Ordnern des NAS zu und von (2-way-sync) bestimmten Endgeräten zu syncen. Das sollte möglich sein, ohne smb, ftp oder sonstiges nativ verwenden zu müssen, um entsprechenden Komfort zu erzeugen. Daten die alltäglich und sofort zwischen Geräten gesynced werden müssen sollten dediziert behandelt werden.

## Möglichkeiten

- syncthing (z.B. [https://github.com/syncthing/syncthing/blob/main/README-Docker.md](https://github.com/syncthing/syncthing/blob/main/README-Docker.md "smartCard-inline") )
  syncthing ist ein Tool das lediglich FileSyncing zwischen Geräten bietet. Es können Ordner und Endgeräte einfach hinzugefügt werden. Das syncing erfolgt nach einem einstellbaren Zeitplan. Außerdem können die Dateien versioniert werden falls gewollt. Dateien liegen hier entsprechend ohne Komprimierung auf dem Volume und syncthing agiert lediglich mit diesen. syncthing muss nicht aktiv getriggert werden, um Dateien zu scannen. Einen direkten Zugriff auf Daten auf dem Server kann durch unraid unproblematisch über smb realisiert werden. Diese Lösung ist also sehr lean und mit minimalem Einfluss auf die Daten an sich.
  Info: Backups der Server-Konfiguration sollte einfach möglich sein. ([https://forum.syncthing.net/t/how-to-backup-syncthing-configuration-and-database/6844/8](https://forum.syncthing.net/t/how-to-backup-syncthing-configuration-and-database/6844/8 "smartCard-inline") )
- pydio (z.B. [https://techviewleo.com/run-pydio-cells-file-sharing-in-docker-container/](https://techviewleo.com/run-pydio-cells-file-sharing-in-docker-container/ "‌"))
  pydio kann als reine File Hosting App wie Seafile genutzt werden. Es kann konfiguriert werden, ob Daten flat oder structured abgelegt werden sollen. Somit ist es mit structured storage möglich Daten nativ auf dem volume lesen zu können, sodass pydio nicht zwingend als Interface für ein Backup oder zur Datengewinnung benötigt wird.
  In pydio können auch beliebige Userfolder gemounted werden. In diesen mounts können Folder dann als Structured Storage in pydio konfiguriert werden.
  Info: Die MobileApp von pydio ist aktuell nicht nutzbar. Logins sind nicht möglich.
  Siehe hier: [https://pydio.com/en/docs/cells/v2/file-system-storage](https://pydio.com/en/docs/cells/v2/file-system-storage "smartCard-inline")
  Siehe hier: [https://pydio.com/en/docs/cells/v3/datasource-format](https://pydio.com/en/docs/cells/v3/datasource-format "smartCard-inline")
- seafile (z.B. [https://manual.seafile.com/docker/deploy_seafile_with_docker/](https://manual.seafile.com/docker/deploy_seafile_with_docker/ "smartCard-inline") )
  Da lediglich File Sharing und Syncing benötigt wird über diese App bietet sich Seafile an. Seafile bietet im Gegensatz zu Nextcloud lediglich das Feature des File Hosting an und läuft angeblich wesentlich stabiler und schneller.
  Info: Nachteil kann sein, dass die Dateien die durch Seafile gehostet werden nicht nativ auf dem Volume gelesen werden können. Dateien werden durch Seafile immer zerlegt und so gespeichert, sodass der Seafile Storage immer gemounted werden muss. Das kann unter umständen umständlich sein und ist problematisch falls Daten bei Komplettverlust des Hauptservers widerhergestellt werden müssen.
- ownCloud
- Nextcloud (z.B. [https://www.wundertech.net/how-to-install-nextcloud-on-unraid/](https://www.wundertech.net/how-to-install-nextcloud-on-unraid/ "smartCard-inline") )
  Nextcloud bietet zusätzlich zum File Hosting viele andere Features wie Kalender, VideoChat, Mailing, ... Dadurch und durch die aktuelle Entwicklungsphilosophie kann Nextcloud zum Teil instabil laufen oder sich gar durch Updates komplett zerstören. Der Container muss dann neu aufgesetzt werden.
  Nextcloud erzeugt eine eigene Dateiumgebung in einem spezifizierten Pfad. Alle Dateien müssen dort liegen, oder das Dockersetup muss angepasst werden
  Info: symlinks funktionieren nicht, um Ordner zu Nextcloud hinzuzufügen! ([https://help.nextcloud.com/t/symlink-inside-data-folder-seems-not-to-work/5973?source\_topic\_id=25877](https://help.nextcloud.com/t/symlink-inside-data-folder-seems-not-to-work/5973?source_topic_id=25877 "‌"))
  Info: Um externe Ordner zu Nextcloud hinzuzufügen, und damit keine Datein im Docker Volumes Ordner zu hosten (könnte Problematisch sein da Docker Dateien dort löschen kann) kann der entsprechende externe Ordner in der Docker Compose File als Volume gemounted werden und muss dann als External Storage über die App External Storage hinzugefügt werden:
  ![Screenshot\_from\_2023-06-30\_13-31-24.png](https://trello.com/1/cards/649ea641aaf24d092f0e9794/attachments/649ebd3a7069437456403bca/download/Screenshot_from_2023-06-30_13-31-24.png)
- Problem: Nextcloud erzeugt eine Database zur Bereitstellung der Dateien die Nextcloud hinzugefügt wurden. Dadurch muss ein Scan durchgeführt werden falls Dateien NICHT durch Nextcloud auf den Server kopiert werden sollen. In Dockerumgebung kann der Command so aussehen: `sudo docker exec -ti --user www-data nextcloud-app /var/www/html/occ files:scan --all`

‌

Beispiel Docker Compose file for Nextcloud:

```
version: '2'

services:
  db:
    image: mariadb:10.5
    restart: always
    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW
    volumes:
      - /var/lib/docker/volumes/Nextcloud_Database:/var/lib/mysql
    environment:
      # Passwörter am besten anpassen!
      - MYSQL_ROOT_PASSWORD=password
      - MYSQL_PASSWORD=password
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud

  app:
    image: nextcloud
    restart: always
    ports:
      - 8080:80
    links:
      - db
    volumes:
      # standard volume, um alle benötigten Datein für Nextcloud bereitzustellen.
      # Standardmäßig werden hier im data-Ordner die Nutzer-Datein gespeichert.
      # Bei möglichen Docker-Updates sollte dieser Ordner aber nciht genutzt werden (persönliche Meinung).
      - /var/lib/docker/volumes/Nextcloud_Application:/var/www/html
      # Für eigene Dateien können Ordner einfach zusätzlich gemounted werden.
      # Z.B. wird hier der Ordner Files eines bestimmten Users nach /mnt/data/ gemounted.
      # Die Zugriffsbeschränkungen müssen dann in Nextcloud mit der
      # External Storage App konfiguriert werden.
      - /mnt/user/data/<user>/files:/mnt/data
      # Es sollten externe Ordner NICHT direkt in /var/www/html-Ordner gemounted werden,
      # da es sonst zu Problemen mit der Nextcloud-App an sich kommt. Diese bekommt so
      # Probleme beim beschreiben der Ordner in /var/www/html aufgrund der
      # Besitzergruppe der extern gemounteten Ordner.
    environment:
      - MYSQL_PASSWORD=password
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_HOST=db
```