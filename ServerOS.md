## Möglichkeiten
proxmox:

- kostenlos
- bietet deutlich bessere Features für Virtualisierung als z.B. unraid (Snapshots, Backup, Passthrough, ...)
- unraid oder trueNAS könnten als VM laufen, um ein NAS aufzusetzen. (am besten mit PCIe Passthrough einer HBA SATA-Erweiterungskarte). Hierfür muss eine HBA-Karte für SATA-Erweiterung genutzt werden, um z.B. unraid sinnvoll zu nutzen.
- nativ können nur LXC Container statt docker genutzt werden. Allerdings kann natürlich eine lightweight Linux VM als Docker VM genutzt werden. 


TrueNAS:

- kostenlos
- evtl. höherer Stromverbrauch, da kein dedizierter idle der HDDs durch ZFS.
- ‌

unraid:

- Falls gewollt: ZFS support ist ab aktueller Version auch verfügbar.

Lizenz mit bis zu 6 Festplatten (60€)

Kann UNRAID mehrere Volumes erstellen?

- Nein. Aktuell nicht. Es wird ein einzelnes Array mit allen zugehörigen Festplatten erstellt. Dort können dann mehrere User Shares erstellt werden die als einzelne Linux mounts dienen. Dadurch kann sowohl ein definierter Benutzerordner erstellt als auch gesonderte Bereiche für spezialiserte Aufgaben (z.B. Surveillance) erstellt werden. Diese können entsprechende Berechtigungen für die User erhalten.

Doku für Storage Management:[https://docs.unraid.net/unraid-os/manual/storage-management/](https://docs.unraid.net/unraid-os/manual/storage-management/ "smartCard-inline")

‌

Festplattengrößen:

- Die Parityfestplatte in unraid muss immer die größte sein. Es kann keine Storage-Festplatte zu unraid hinzugefügt werden die größer ist als die kleinste Parity-Festplatte!
- Der Cache kann mit SSDs versehen werden und wird intelligent genutzt. Sodass immer Schrittweise Daten im Cache abgespeichert werden und erst später auf das Array geschrieben werden. Dadurch kann es Sinn machen auch den Cache mit einer Parity-Disk auszustatten (zweite SSD), um Datenverlust zu vermeiden.