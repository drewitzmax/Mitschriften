# Session 6
## Erläutern Sie das folgende SQL-Statement: select Titel from Bücher where ISBN in (select ISBN from Empfiehlt). Wie funktioniert in SQL die Schachtelung von Anfragen ohne Verzahnung?
select titel -> Gib das Attribut Titel

from Bücher ->  aus der Tabelle Bücher

where ISBN in -> wenn die ISBN in einer gegebenen wertemenge vorhanden ist

veschachteltete Abfrage

select ISBN -> Gib das Attribut ISBN

from Empfiehlt -> azs der Tabelle Empfiehlt

=> Liste aller Buchtitel, die in der Empfiehlt Tabelle empfohlen wurden 
### Auswertungsschritte ohne Verzahnunhg
1. Innere Abfrage auswerten
2. Ergebnis in die äußere Abfrage einsetzen (Menge von Konstanten)
3. Die äußere Abfrage wird ausgewertet

## Erläutern Sie das folgende SQL-Statement: select Nachname from Personen where 1.0 in (select Note from Prüft where PANr = Personen.PANr). Wie funktioniert in SQL die Schachtelung von Anfragen mit Verzahnung?

select Nachname -> Gib das Attribut Nachname

from Personen -> aus der Tabelle Personen

where 1.0 in -> Wenn der Wert 1.0 in einer gegebenen Wertemenge vorhanden ist

verschachtelte Abfrage

select Note -> gib das Attribut Note

from Prüft -> aus der Tabelle Prüft

where PANr = Personen.PANr -> Wenn die PANr der Prüft Tabelle mit der PANr aus der Personen Tabelle übereinstimmt
### Auswertungsschritte mit Verzahnung
1. Das erste Tupel der äußeren Abfrage wird untersucht
2. Tupel wird in die innere Abfrage eingesetzt
3. Die innere Abfrage wird ausgewertet
4. Das Ergebnis wird in die äußere Abfrage eingesetzt
5. Die äußere Abfrage wird für das aktuelle Tupel ausgewertet => das Tupel ins Ergebenis übernommen oder verworfen
6. Für jedes weitere Tupel die Schritte wiederholen

### Besser
NATURAL JOIN verwenden

select Nachname from Personen natural join Prüft where Note=1.0 and Personen.PANr=Prüft.PANr

Es werden alle Nachnamen von Personen geliefert, die eine Prüfung mit der Note 1.0 absolviert haben
### Frage
Werden solche Anfragen automatisiert durch moderne DBMS optimiert?

## Liegt bei dem folgenden Statement eine Verzahnung vor? select Matrikelnummer from Prüft where PANr in (select PANr from Prüft where Matrikelnummer = '8625510'). Was bedeutet dieses Statement?
- Es wird auf die gleiche Tabelle zugegriffen
- Die innere Abfrage kann unabhängig vom Tupel der äußeren Abfrage ausgewertet werden
- Es besteht keine Verzahnung der Abfragen

Es wird die Matrikelnummer 8625510 geliefert, wenn der Entsprechende Student ein zugehöriges Tupel in der Prüft Tabelle hat und die PANr definiert ist.