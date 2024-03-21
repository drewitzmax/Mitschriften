# Session 5
## 5 Buch & Buchexemplar
```
CREATE TABLE Buch (Title varchar(100), ISBN varchar(20), PRIMARY KEY(ISBN));
CREATE TABLE Buch_Exemplar (InvNr integer, Kaufdatum date, ISBN varchar(20), CONSTRAINT fk_isbn FOREIGN KEY(ISBN) REFERENCES Buch(ISBN));
```
## 6 Professor & Lehrstuhl
```
CREATE TABLE LSt (Bez varchar(100), AnzPst integer, PRIMARY KEY(Bez));
CREATE TABLE Prof_hat (PANr integer, Stufe integer, Bez varchar NOT NULL, PRIMARY KEY(PANr), CONSTRAINT fk_bez FOREIGN KEY(Bez) REFERENCES LSt(Bez));
```
## 7 Vorlesung & Voraussetzung
```
CREATE TABLE VO (VNr integer, VBez varchar(100), PRIMARY KEY(VNr));
CREATE TABLE setzt_voraus (vorher integer, nachher integer, PRIMARY KEY(vorher, nachher), CONSTRAINT fk_vorher FOREIGN KEY(vorher) REFERENCES VO(VNr), CONSTRAINT fk_nachher FOREIGN KEY(nachher) REFERENCES VO(VNr));
```

## 8 Professor IST Mitarbeiter IST Person
```
CREATE TABLE Person(SVNr char(10), p_name varchar(50), PRIMARY KEY(SVNr));
CREATE TABLE Mitarbeiter(PANr integer NOT NULL UNIQUE, EDat date, SVNr char(10), PRIMARY KEY(SVNr), CONSTRAINT fk_svnr FOREIGN KEY(SVNr) REFERENCES Person(SVNr));
CREATE TABLE Prof(SVNr char(10), Stufe varchar(20), PRIMARY KEY(SVNr), CONSTRAINT fk_svnr FOREIGN KEY(SVNr) REFERENCES Mitarbeiter(SVNr));

```

## 9 DROP und ALTER TABLE Statements 
### DROP TABLE
`DROP TABLE {tablename};`
- löscht die gesamte tabelle
- danach -> Datenbak muss in validem state sein
- cascades beachten
- gegbenenfalls abhängige Tabellen vorher manipulieren
- Alternativ "TRUNCATE" löscht inhalt der Tabelle
### ALTER TABLE
```
ALTER TABLE
    ADD column_name datatype
    DROP COLUMN column_name
    RENAME COULUMN old_name TO new_name
```