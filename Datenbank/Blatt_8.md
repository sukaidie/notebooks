## Aufgabe 1

1. Geben Sie die folgenden DDL - Statements an
```sql
  CREATE TABLE Mitarbeiter (
	IDperson    	     INTEGER PRIMARY KEY,
	IDabteilung 	     INTEGER REFERENCE Abteilung(IDabteilung),
	personNr    	     INTEGER UNIQUE NOT NULL,
	stellenbezeichnung VARCHAR(25),
	datumEinstellung   DATE,
	gehalt 	    	     INTEGER,
	raumNr 			       VARCHAR(9),
	durchwahl 		     VARCHAR(4));

  CREATE VIEW PatientenTelephonebuch AS
  SELECT IDperson,vorname,nachname,zimmerNr,durchwahl,datumAufname
  FROM Patientenaufenthalt NATURAL JOIN Person
  WHERE datumEntlassung IS NULL
```

2. Formulieren Sie, basierend auf dem oben gezeigten DB-Schema, die folgenden SQL -  Statements.
```sql
a) SELECT COUNT(*)
   FROM PatientenTelephonebuch
   WHERE DATE datumAufname + INTERVAL 1 MONTH < CURRENT_DATE

b) SELECT vorname,nachname,gehalt
   FROM Mitarbeiter NATURAL JOIN Person
   WHERE datumEintellung >= ALL(
	    SELECT datumEintellung
	    FROM  Mitarbeiter)

c) SELECT *
   FROM Mitarbeiter NATURAL JOIN Person
   WHERE IDabteilung IN(
	     SELECT IDabteilung
	     FROM Abteilungen JOIN Person
           ON(Abteilungen.IDpersonChefarzt = Person.IDperson)
	     WHERE vorname = 'Klaus' AND nachname = 'Kunstfehler')

d) INSERT INTO
   Abrechnungen(IDabrechnung, IDaufenthalt, datumAbrechung, betragErhalten )
   VALUES(123, 333, CURRENT_DATE, 0)

   UPDARE Abrechnungen
   SET euroSumme = SELECT SUM(euroSumme) FROM Behandlungen WHERE IDaufenthalt = 333
   WHERE IDabrechnung = 123

e) SELECT IDperson
   FROM Patientenaufenthalte NATURAL JOIN Behandlungen
   GROUP BY IDperon,IDaufenthalt
   HAVING COUNT(DISTINCT IDabteilung) > 3  

f) SELECT SUM(euroKosten)
   FROM Abrechnungen
       NATURAL JOIN Patientenaufenthalte
       NATURAL JOIN Person
       NATURAL JOIN Versicherungen
   WHERE EXTRCT(YEAR FROM datumAufname) = 2010
       AND betragErhalten = 1
       AND name = 'BBK'
       AND IDperson NOT IN (SELECT IDperson FROM Mitarbeiter)
```

## Aufgabe 2016

```sql
/*  Gib Sie alle Paare aus*/
SELECT *
FROM couple
JOIN character male on(couple.maleid = male.characterid)
JOIN character female on(couple.femaleid = female.characterid);

/*Füge Rainer Unland mit der ID 500 in die Tabelle character ein. */
INSERT INTO character(characterid, firstname, lastname)
VALUES(500, 'Rainer', 'Unland');

/*Verheirate Rainer Unland mit sich selbst!*/
INSERT INTO couple
VALUES(500, 500, 500);

/*Lösche die beiden gerade definierten Paare.*/
DELETE FROM couple
WHERE coupleid = 500 or coupleid = 501;

/*
 * Selektiere alle Paare,
 * in der eine Person als Frau eingetragen ist,
 * obwohl es sich um einen Mann handelt
 */
SELECT coupleid
FROM couple
JOIN character on(couple.femaleid = character.characterid)
NATURAL JOIN gender
WHERE gender = 'male';

/* Definiere einen Constraint,
 * sodass die vorherig falsch eingetragenen Paare sich
 * nicht mehr in der Datenbank befinden können
 */
ALTER couple
ADD CONSTRAINT noselfmarriage CHECK(femaleid != maleid);
```
