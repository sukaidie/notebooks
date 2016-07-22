**Datenbanksystem** | Übungsblatt 06

### Aufgabe 2

2, 3, 4, 5, 7

### Aufgabe 3

```sql
a. SELECT studienfach, COUNT(*)
   FROM Student
   GROUP BY studienfach

b. SELECT *
   FROM Student NATURAL JOIN Person
   ORDER BY studienfache, nachname ASC, vorname

c. SELECT fachbereich, COUNT(*)
   FROM Student
   GROUP BY fachbereich
   HAVING COUNT(*) < 2

d. SELECT studientfach, AVG(note)
   FROM Student NATURAL JOIN Leistung
   WHERE fachbereich = 'DBMS'
   GROUP BY studienfach

e. SELECT vorname, nachname, matrikelnummer, COUNT(lv_nr)
   FROM Student NATUTAL LEFT JOIN Person NATURAL JOIN Leistung
   GROUP BY vorname, nachname, matrikelnummer
   ORDER BY nachname ASC, vorname ASC
```

### Aufgabe 4

```sql
a. SELECT raum Mitarbeiter
   UNION
   SELECT FROM Lehrveranstaltung

b. SELECT vorname, nachname
   FROM Student
   WHERE personID IN (
   SELECT personID FROM Mitarbeiter)

c. SELECT personID, gehalt
   FROM Mitarbeiter
   WHERE NOT EXISTS (
   SELECT personID FROM Student
   WHERE Mitarbeiter.personID = Student.personID)

d. SELECT personID
   FROM Student
   WHERE personID IN (
   SELECT personID
   FROM Leistung
   WHERE note <= 2.0)

e. SELECT Martrikelnummer
   FROM Student
   WHERE personID 4.0 <= ALL (
   SELECT note
   FROM Leistung
   WHERE Student.personID = Leistung.personID)
```

### Zusatzaufgabe 1

```sql
a. CREATE TABLE Student (
       personID       INTEGER PREMARY KEY,
       matrikelnummer INTEGER UNIQUE NOT NULL,
       fachbereich    VARCHAR(25),
       studienfach    VARCHAR(25),
       fachsemester   INTEGER,
       CONSTRAINT fk
           FOREIGN KEY (personID) REFERENCES Person(personID)
       CONSTRAINT matrikelnr
           CHECK (matrikelnummer BETWEEN 0000000 AND 9999999)
       CONSTRAINT studien
           CHECK (studienfach IN ('SE', 'Wiinf', 'Mathe', 'Chemie'))
   );

   CREATE TABLE Lehrveranstaltung (
       lv_nr         INTEGER PREMARY KEY,,
       raum          INTEGER NOT NULL,
       gehalten_seit INTEGER,
       status        CHAR(2) CHECK (value IN ('GS', 'HS'),
   );

b. ALTER TABLE Leistung
       ADD COLUMN Punktzahl INTEGER

   ALTER TABLE Lehrveranstaltung
       ADD CONSTRAINT raum
       CHECK (raum NOT IN (SELECT raum FROM Mitarbeiter))

c. DROP TABLE Betreuung
```

### Zusatzaufgabe 2

```sql
a. INSERT INTO Person
   VALUES(SELECT MAX(personID) + 1 FROM Person, 'Klaus', 'Newman');
   INSERT INTO  Mitarbeiter
   VALUES(SELECT personID, 16, 2000, 'SH402' FROM Person WHERE vorname = 'Klaus')
b. UPDATE Betreuung
   SET personID = (SELECT personID FROM Person WHERE vorname = 'Klaus' AND nachname = 'Newman')
   WHERE lv_nr = (
     SELECT lv_nr
     FROM Betreuung
     NATURAL JOIN Lehrveranstaltung
     NATURAL JOIN Person
     WHERE vorname = 'Karl' AND nachname = 'Oldman'
     and gehalten_seit >= '2009-05-30'
   )
c. DELETE Mitarbeiter
   WHERE personID = (
     SELECT SELECT personID FROM Person WHERE vorname = 'Klaus' AND nachname = 'Newman'
   );
   DELETE Betreuung
      WHERE personID = (
        SELECT SELECT personID FROM Person WHERE vorname = 'Klaus' AND nachname = 'Newman'
   );
   DELETE Person
      WHERE personID = (
        SELECT SELECT personID FROM Person WHERE vorname = 'Klaus' AND nachname = 'Newman'
   );
```
