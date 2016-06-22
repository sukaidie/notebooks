**Datenbanksystem** | Übungsblatt 01

1. Was ist eine Datenbank?

 * Eine Datenbank ist eine integrierte Ansammlung von Daten, die allen Benutzern eines Anwendungsbereiches als gemeinsame Basis aktueller Information dient. Die Daten sind entsprechend den natürlichen Zusammenhängen strukturiert, so daß für jede - auch ungeplante - Anwendung in der für sie benötigten Weise auf die Daten zugegriffen werden kann.

2. Welche Aspekte sind für Datenbanken(und die darauf basierenden Informationssysteme) wichtig?

 * Entkopplung der Anwendungsprogramme von den pysischen Spreicherstrukturen der Daten(“Datenunabhängigkeit von Anwendungsprogramme”)
 * (Datenbak-)”Datenmodelle”: angebotene logische Datenstrukturen und Operationen (relationale , hierachiches Netzwerk-Datenmodell)
 * Entwurf eines Informationssystems
 * Semantische Datenmodelliserung
    - Konkreter Datenbankentwurf
    - Kriterien für “guten” Datenbankentwurf
    - Systemseitige Gewährleistung der Integrität der Daten
 * (Interne) Speicherstrukturen der Daten auf externspeicher und Mittel zur Beschlaunigung des Zugriff auf die Daten
 * Mehrbenutzerbetrieb und Fehlertolerenz
 * Vermeidung von Fehlern durch Parallelausführung von Datenbanksbefehlen(Sychronisation)
 * Maßnahmen gegen Datenverlust und Fehler in der Datenbank durch Programmfehler, Programm- und Systemabstürz
 * Widerherstellung eines konsisteten Datenbank-Zustandes nach solchen Ereignissen(Recovery)

3. Was bedeutet „Integrität der Daten“?

 * Keine widerspruchlichen Angaben sowie keine ungültigen Verweise in der Datenbank(Zentrale Konsistenzüberwachung)

4.  Beschreiben Sie die generelle Struktur von Datenbanksystemen.

5.  Beschreiben Sie die ANSI/SPARC 3-Schema-Architektur. Welche Ziele werden durch diese verfolgt?
 * Externes Schema: Benutzersichten
 * Konzeptuelles Schema: stabiles globales Referenzschema(Beziehungen und Semantik der Daten)
 * Internes Schema: pysische Realisierung
 * Ziel: möglichst weitgehende Vermeidung von Abhängikeiten zwischen Anwendungsprograme und pysischer Datenspeicherung.  Trennung der semantischen Datensicht von der physischen Speicherung (Speicherstruktur) der Daten

6.  Was bedeutet logische und physische Datenunabhängigkeit ?
 * Pysiche Datenunabhängigkeit: Isolation der Anwendungsprogramme von Änderungen der pysischen Datenorganisation und des Zugriffs(z.B. Änderung der Datenorganisation, Einfügen eines Zugriffspfades. Etc)
 * Logische Datenunabhängigkeit: Isolation der Anwendungsprogramme von Änderungen der logischen Darstellung der Daten innerhalb der Datenbamk(z.B. Hinzufügen von neuen Attributen, Umnennung der Attributen)

7.  Erläutern Sie die Begriffe
 * **Persistenz,** dauerhafte Speicherung von Daten
 * **Synchronisation**, sicheres gleichzeitiges Arbeiten auf dem gemeinsamen Datenbestand
 * **Recovery**, zentrale, automatische Fehlerbehandlung und Fehlerbehebung
 * **Integrität**, zentrale Konsistenzüberwachung
 * **Abfragesprache**, assoziativer (inhaltsbezogener) Zugriff auf Daten
 * **Autorisierung**, zentrale Zugriffskontrolle
