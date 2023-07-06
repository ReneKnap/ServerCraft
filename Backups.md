## Lokale Backups

### MacOS

#### Time Machine
- Alle Daten und Systemeinstellungen werden gespiegeln
- Bootable
- Inkrementelle Snapshots
- Viele Einstellmöglichkeiten
- NAS kompatible
- Kostenlos

### Linux

#### Timeshift
- [github/timeshift](https://github.com/teejee2008/timeshift)
- Ähnlich wie [Time Machine](Backups#MacOS#Time Machine)
- <span style="color: red;">Benutzerdateien wie Dokumente, Bilder und Musik sind ausgeschlossen.</span>
- Im RSYNC Modus werden Snapshots mit [rsync](http://rsync.samba.org/) und Hardlinks erstellt. Gemeinsame Dateien werden von den Snapshots gemeinsam genutzt, was Festplattenplatz spart. Jeder Snapshot ist eine vollständige Systemsicherung, die mit einem Dateimanager durchsucht werden kann.
- Im BTRFS-Modus werden Snapshots mit den integrierten Funktionen des BTRFS-Dateisystems erstellt. BTRFS-Snapshots werden nur auf BTRFS-Systemen mit einem Ubuntu-artigen Subvolume-Layout (mit @- und @home-Subvolumes) unterstützt.
- Kostenlos

#### rsnapshot
- [rsnapshot](https://rsnapshot.org/)
- Ähnlich wie [Time Machine](Backups#MacOS#Time Machine)
- rsnapshot ist ein Dienstprogramm für Dateisystem-Snapshots, das auf rsync basiert. rsnapshot macht es einfach, periodische Snapshots von lokalen und entfernten Rechnern über ssh zu erstellen. Der Code macht, wann immer es möglich ist, ausgiebig Gebrauch von Hardlinks, um den benötigten Speicherplatz zu reduzieren.
- Kostenlos

#### backintime
- [github/backintime](https://github.com/bit-team/backintime)
- Ähnlich wie [Time Machine](Backups#MacOS#Time Machine)
- Einfach zu bedienendes Backup-Tool für Dateien und Ordner
- Kostenlos

#### TimeVault
- [TimeVault](https://wiki.ubuntu.com/TimeVault)
- Snapshots
- <span style="color: red;">unmaintained</span>
- Kostenlos

#### Duplicity
- [duplicity](https://duplicity.us/)
- Duplicity sichert Verzeichnisse, indem es verschlüsselte Datenträger im Tar-Format erstellt und diese auf einem remote oder lokalen Server hochlädt. 
- Da duplicity librsync verwendet, sind die inkrementellen Archive platzsparend und zeichnen nur die Teile der Dateien auf, die sich seit der letzten Sicherung geändert haben. 
- Duplicity verwendet GnuP , um diese Archive zu verschlüsseln.
- Das duplicity-Paket enthält auch das Dienstprogramm rdiffdir. 
- Kostenlos

### Windows

#### Windows 10 +
- Datei-Backup mit dem integrierten Windows-Dateiversionsverlauf
	- Funktion namens "Dateiversionsverlauf"
	- regelmäßig automatische Backups von Dateien und Ordnern
	- "Einstellungen" > "Update und Sicherheit" > "Sicherung" > "Dateiversionsverlauf"
	- Format VHD (Virtual Hard Disk)
- Systemabbild-Backup mit der Windows-Sicherung
	- vollständiges Systemabbild
		- gesamten Inhalt Ihrer Festplatte einschließlich des Betriebssystems und aller installierten Programme erfasst.
	- "Einstellungen" > "Update und Sicherheit" > "Sicherung" > "Systemabbild sichern"
	- Format ".vhd" oder ".vhdx"

#### Acronis True Image
- [Acronis True Image](https://www.acronis.com/en-us/)
- <span style="color: red;">49€/Jahr</span>

#### AOMEI Backupper Standard
- [AOMEI Backupper Standard](https://www.aomeitech.com/ab/standard.html)
- Vollständiges Backup des Windows-Betriebssystems
- Backup der gesamten Festplatte, Partitionen und einzelnen Dateien
- Individualisierte Backup-Einstellungen:
    - Regelmäßige Backups
    - Erstellung inkrementeller Backups
    - Backup komprimieren und aufteilen
- Kostenlos

#### EaseUS Todo Backup
- [EaseUS Todo Backup](https://www.easeus.com/backup-utility/windows-11-backup-to-nas.html)
- Kostenlos
- Sichern von Dateien, System, Festplatten/Partitionen und Mails.
- Ein-Klick-Backup spart Zeit und Lernkosten in höchstem Maße
- Unterstützt Benutzer, um Backups überall zu speichern: lokale Laufwerke, NAS, und Cloud
