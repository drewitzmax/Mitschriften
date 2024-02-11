# DB Session 1
## (F) Warum braucht man Datenbanken? Erläutern Sie das Problem der Datenredundanz.
- zentrale Datenhaltung
- effiziente Zugriffe auf Daten
- eliminierung von Datenredundanz
  - Dateien werden an mehreren Orten gleichzeitig gehalten (verfügbarkeit/ unnötiger Speicherverbrauch)
  - Dateien liegen in verschiedenen Versionen vor (fehlende Synchronization)
## (F) Welche Aufgaben hat ein Datenbankmanagementsystem (Regeln von Codd)?
1. Integration
    - einheitliche verwaltung der Daten (redundanzvermeidung)
2. Operation 
    - CRUD operationen
3. Katalog - Data Dictionary
    - Halten einer Datenbankbeschreibung mit Relationen und typen der Datenbank
4. Benutzersichten
    - Implementierung verschiedener Darstellungen für spezielle Anwendungen
5. Konstistenzüberwachung
    - Sicherstellung der Integrität der Daten.
    - Kollisionen
    - Nicht vollständige Updates
6. Zugriffskontrolle
    - Beschränkung des Zugriffs auf die Datenbank
    - Sicherheit der Vertraulichkeit der Daten
7. Transaktionen
    - Bündelung mehrerer Statements die zusammen (als ganzes) ausgeführt werden.
    - Sicherstellung aller updates
    - Rollback aller Statements bei Fehler
8. Synchronization
    - Vermeidung von Schreibkonflikten
    - Vermeidung von Seiteneffekten verschiedener Transaktionen aufeinander
9.  Datensicherung
    - Sicherung der Wiederherstellbarkeit der Daten im Fehlerfall

## (F) Geben Sie Klassifikationen für Integritätsbedingungen an (z.B. statisch, transitional, temporal, etc...) und erläutern Sie diese anhand von Beispielen.

## (F) Erläutern Sie die Schema-Architektur und die Arten der Datenunabhängigkeit.

## (F) Erläutern Sie die grundlegende System-Architektur von Datenbanksystemen (ANSI-SPARC).

## (F) Erläutern und vergleichen Sie mögliche Anwendungsarchitekturen.

## (F) Erläutern Sie verschiedene Architekturen zur Integritätssicherung und stellen Sie die jeweiligen Vor- und Nachteile einander gegenüber.

## (F) Was ist eine Transaktion? Erläutern Sie die ACID Eigenschaften. Beschreiben Sie anhand eines Beispiels (z.B. Flugbuchung), warum Transaktionen von Bedeutung sind bzw. was ohne Transaktionen bzw. ohne die einzelnen ACID-Eigenschaften passieren könnte.