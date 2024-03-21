# Session 4

## Worin besteht die Entwurfsaufgabe einer Datenbank? Welche Eigenschaften muss der Entwurfsprozess aufweisen (formal und informell)?
## Welche Phasen sind beim Datenbankentwurf von Bedeutung? Beschreiben Sie die wichtigsten Punkte der einzelnen Phasen.
### Anforderungsanalyse
- Erhebung des Informationsbedarfs
- Beschreibung des fachlichen Problems
- (Daten und Funktionsanforderungen trennen)
### Konzeptioneller Entwurf
- modellierung der Sichten
- Analyse Konflikte
  - Namen, Typ, Wertebereich, Bedingung, Struktur
- Intergration in ein Gesamtschema
- Ergbenis: komplexes Gesamtschema (z.B. ER-Diagram)
### Verteilungsentwurf
- horizontale Fragmentierung
  - tupel auf verschiedenen Knoten 
- vertikale Fragmentierung  
  - aufteilung der daten auf verschiedene Schemata

### Logischer Entwurf
- umsetzung in das Zieldatenbankmodell
- Verbesserungen, optimierung(zugriffsgeschwindigkeit vs redundanzfreiheit), normalisierung (minimale Redundanz)
- => logisches Schema (Sammlung von Relationen)
### Datendefinition

### Physischer Entwurf
### Implementierung und Wartung

## Erläutern Sie die Anforderungsanalyse und den konzeptionellen Entwurf. Beschreiben Sie jene Konflikte, die auftreten können, wenn im Rahmen des konzeptionellen Entwurfes die modellierten Sichten der verschiedenen Anwender in eine Gesamtsicht integriert werden sollen.
## Was bedeuten vertikale und horizontale Fragmentierung beim Relationenmodell und was muss man dabei beachten?
### Horizontale Fragmentierung
- Tupel einer Relation/Tabelle auf Relationen/Tabellen mit gleichem Schema
- Aufteilung auf Knoten (Last verringerung)
- Potenziell bessere Performance bei lesenden Zugriffen
- Höhere Komplexität der Integritätsvalidierung bei schreibenden Zugriffen
- Möglichkeit sensible Daten abzuspalten (spezielle Nutzer oder Anwendungen)
## Was ist der Unterschied zwischen ER-Modell und Relationenmodell. Warum braucht man überhaupt zwei verschiedene Modelle?
## Was bedeutet bei der Transformation vom ER-Modell ins Relationenmodell die Forderung nach Erhaltung der Informationskapazität? Geben Sie je ein Beispiel für eine kapazitätserhöhende und eine kapazitätsvermindernde Abbildung an.
## Formen Sie eine zweistellige n:m-Beziehung vom ER-Diagramm in das relationale Schema um. Diskutieren Sie mögliche Varianten.
## Formen Sie eine zweistellige 1:n-Beziehung vom ER-Diagramm in das relationale Schema um. Diskutieren Sie mögliche Varianten.
## Formen Sie eine zweistellige 1:1-Beziehung vom ER-Diagramm in das relationale Schema um. Diskutieren Sie mögliche Varianten.