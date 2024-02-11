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
Kriterium Klassen
### Granularität Attribut
- Tupel
- Relation
- Datenbank
### Ausdrucksfähigkeit
- elementare Prädikate
- Relationenalgebra
- SQL
- SQL + transitive Hülle
- berechnungsvollständig
### zeitlicher Kontext
- statisch
- transitional
- temporal
### Überprüfungszeitpunkt
- Einzeländerung
- Operationsende
- Transaktionsende
### Reaktion
- Zurückweisung (reject)
- Korrektur (repair)

## (F) Erläutern Sie die Schema-Architektur und die Arten der Datenunabhängigkeit.
### konzeptuelle Schema
- Datenmodell und Definition
### interne Schema
- Interne verwaltung der Daten
- Dateiorganisation
- Zugriffspfade
### externe Schema
- Sichtdefinitionen - Benutzeransichten

## (F) Erläutern Sie die grundlegende System-Architektur von Datenbanksystemen (ANSI-SPARC).
Die Systemarchitektur von Datenbanksystemen lässt sich in 4 Komponenten gliedern
### Definitionskomponenten
### Programmierkomponenten
### Benutzerkomponenten
### Transformationskomponenten
Transformationskomponenten sind für die 

## (F) Erläutern und vergleichen Sie mögliche Anwendungsarchitekturen.
Vorrangig existiert eine Server-Client Architektur im bereich der datenbankbasiereten Systeme. 
### 2-Schichten-Architektur
Es werden 2 Anwendungsschichten verwendet:
1. Ein Anwenderprogramm, dass die Schnittstelle für den User, die Businesslogik der Software und die Schnittstelle zur Datenbank beinhaltet
2. Das DBMS
### 3-Schichten-Architektur
1. Eine Client-Anwendung, die als Schnittstelle für den Benutzer dient.
2. Ein Applikationsserver, der die Businesslogik der Applikation implementiert und als Schnittstelle zur Datenbank fungiert.
3. DBMS
### Vergleich
- Bei der 2SA wird potentiell mehr redundanter Code produziert
- höherer Entwicklungsaufwand bei 3SA, wenn nicht mehrfach verwendet
- 2SA schlechter skalierbar
- 2SA höhrerer Wartungsaufwand bei mehreren Applikationen


## (F) Erläutern Sie verschiedene Architekturen zur Integritätssicherung und stellen Sie die jeweiligen Vor- und Nachteile einander gegenüber.
### Integritätssicherung durch Anwendung
Die Integritätssicherung wird durch die Client-Anwendungen der Datenbank durchgeführt. Es kann jede Überprüfung durchgeführt werden, die durch die Entsprechende Programmiersprache ermöglicht wird.
#### Pro
- Unabhängig von den Funktionaliäten des DBMS
- Flexibel durch die Möglichkeiten der Programmiersprache
#### Contra
- Nicht zentral geregelt
- Redundanter Code bei mehreren nutzenden Programmen
- Redundanter Code in verschiedenen Versionen
### Integritätsmonitor als Komponente des DBMS
#### Pro
- Zentrale Handhabung der Überprüfungen
- Unabhängig von Änderungen des Internen Datenbankschemas
- Optimierung durch das DBMS ohne Anpassungen am Programm
#### Contra
- Stark eingeschränkte komplexität der Überprüfungen
### Integritätssicherung durch Einkapselung
Es wird eine Zwischenschicht eingeführt, durch die alle Transaktionen zum DBMS in einer standardisierten Form durchgeführt werden, in der die Konsistenz der Daten zentral durchgeführt wird.
#### Pro
- Die Routinen zur Überprüfung werden Zentral verwaltet
- Unabhängig von den Funktionaliäten des DBMS
- Flexibel durch die Möglichkeiten der Programmiersprache
#### Contra
- Unflexibel bei Änderungen der Validierung (keine Ad-hoc-Änderungen)

## (F) Was ist eine Transaktion? Erläutern Sie die ACID Eigenschaften. Beschreiben Sie anhand eines Beispiels (z.B. Flugbuchung), warum Transaktionen von Bedeutung sind bzw. was ohne Transaktionen bzw. ohne die einzelnen ACID-Eigenschaften passieren könnte.
Eine atomare Folge von Datenbankoperationen
### ACID
#### Atomicity
Die aufteilung der Operationen einer Transaktion ist nicht möglich. Alle Teile werden ausgeführt oder keiner.
(Flugticket buchung und Rechnung werden in einer Transaktion angelegt. Sollte einer von beiden Datensätzen nicht geschrieben werden können wir auch der andere nicht übernommen.)
#### Consistency
Der Zustand nach der Transaktion muss zulässig sein (Constraints)
(Ein neuer Nutzer versucht einen bereits verwendeten Nutzernamen zu verwenden. Nutzernamen müssen laut Datenbankdefinition jedoch einzigartig sein. Die Datenbank ist nicht mehr konsistent und die Transaktion wird abgebrochen und keine der anderen Änderungen übernommen.)
#### Isolation
Transaktionen beeinflussen sich nicht gegenseitig.
(Zwei Nutzer führen parallel eine Registrierung mit dem gleichen Nutzernamen aus. Es kann nicht passieren, dass Transaktion A die bereits geschriebenen Daten von Transaktion B aufgrund des gleichen Schlüssels beinflusst.)
#### Duratbility
Die Auswirkungen einer Transaktion sind persistent
(Ein Sitzplatz auf einem Flug wurde gebucht. Die Daten sind definitiv geschrieben und werden von allen anderen Transaktionen berücksichtigt. Die Daten sind ohne explizite Löschung oder Änderung durch eine andere Transaktion nicht veränderlich.)