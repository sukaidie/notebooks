## 1.0 Einführung

* ANSI-3 3-Ebene Modell
  * Externe Schema
  * Konzeptuelles Schema
  * Internes Schema

## 2.0 Data Model and Types

* ER Diagramm
  * **1:1, 1:N, N:M**
  * Martin Notation
  * ![](https://dl.dropboxusercontent.com/u/55616012/note/erp.svg)

## 3.0 Ableitung eines Schemas aus ER-Diagramm

* Glossar
  * Klassfikation : 分类
  * Assoziation : 关联
  * Aggregation : 聚合
  * Composition : 合成
  * Generalisierung
  * Aggregation implies a relationship where the child can exist independently of the parent. Example: Class (parent) and Student (child). Delete the Class and the Students still exist.
  * Composition implies a relationship where the child cannot exist independent of the parent. Example: House (parent) and Room (child). Rooms don't exist separate to a House.

* 1: N : write 1 to N as Foreign Key
* N: M : muss dazu eine Tabelle erstellt werden

## 4.0 Normalformen

1NF： 数据库表的每一列都是不可分割的基本数据项
*Attribtte should be automar.*

2NF : 普通键依赖全部候选键，即一组候选（主）键构成超键可以标示唯一实例
*it does not exist functional dependencies between normal keys and candidate keys (UNIQUE).*

3NF ： 普通键之间没有函数关系
*it does not exist functional dependencies between normal keys.*

**Bedingung zur Zerlegung**
* Abhängigkeitstreue
* Verbundstreue

**key type**
* normal key
* candidate key (UNIQUE)
* primary key (UNIQUE, NOTNULL)
* foreign key


## 6.5 Relationale Algebra

* Relation
  * keine Duplikate
  * Keine Reihenfolge
* Mengenoperationen
  * **Kartesisches Produkt**
    * kommutativ
    * assoziativ
    * ( CROSS ) JOIN 的顺序及优先级不影响结果表
  * **Vereinigung**
  * **Differenz** EXCEPT
  * **Durchschnitt** INTERSECT
* Relationale Operationen
  * **Selektion**
  * **Projektion**
* Makrooperationen
  * **Division**
  * **(Innerer) Verbund**
    * Kombination aus Kartesischem Produkt, Selektion nach Verbundbedingungen
    * kommutativ und assoziativ
  * **Thetaverbund**
  * **Gleichverbund**
  * **Natürlicher Verbund**
  * **Semiverbund**

## 7.2 Datendefinitionsprache

### Datentypen

* Char
  * fixed
  * var
* Time
  * TIMESTAMP
  * DATE
  * TIMES
  * INTERVAL
* Bit
  * fixed
  * var
* Nummer
  * SMALLINT
  * INTEGER
  * DECIMAL
  * NUMERIC
  * REAL
  * FLOAT
  * DOUBLE

### Prädikate

* **BETWEEN** ( Alle Typen )
```sql
BETWEEN DATE '2001-09-11' and DATE '2011-10-01'
```
* **IN** ( Alle Typen )
* **LIKE** ( String )
```sql
LIKE 'M%'
LIKE 'M__R'
```
* **NULL** ( Alle Typen )
* **OVERLAPS** ( Interval )
```sql
(TIME'09:00:00', INTERVAL'-50' MINUTE) OVERLAPS (TIME'02:15:00', INTERVAL'6' HOUR)
```

### Benutzerdefinierte Wertbreiche

* **Anlegen Wertbreich**
```sql
 CREAT DOMAIN DOMAIN_NAME AS INTEGER
 DEFAULT '000'
 CONSTRAINT CONSTRAINT_NAME
     CHECK ( VALUE BETWEEN 000 AND 999 )
 DEFERABLE INITIALLY IMMEDIATE;
```
* **CONSTRAINT STATE ::=**
```sql
 NOT DEFERABLE
 DEFERABLE INITIALLY { DEFERRED | IMMEDIATE }
```
* **SET CONSTRAINTS** Clausel
```sql
 SET CONSTRAINTS CONSTRAINTS_NAME { DEFERRED | IMMEDIATE }
```
 SET CONSTRAINTS 会覆盖 DEFERABLE INITIALLY { DEFERRED | IMMEDIATE } 的设定，用于管理员指定的类型验证时间点

### Integritätsbedingungen

NOT NULL
UNIQUE (Schlüsselkandidaten)
PRIMARY KEY (Primärschlüssel, UNIQUE AND NOT NULL)
FOREIGN KEY (Fremdschlüssel)
CHECK
DEFAULT

### Anlegen Tabelle
```sql
 CREATE TABLE TableName (
    domainName INTEGER      PRIMARY KEY,
    domainName VARCHAR(255) NOT NULL,
    domainName DATE         UNIQUE DEFAULT '1970-12-01',
    domainName CHAR(6)      CHECK(VALUE IN | BETWEEN ...),
    CONSTRAINTS fk
         FOREINGN KEY (domainName) REFERENCE TableName
             ON UPDATE CASCADE
             ON DELETE SET NULL
    CONSTRAINTS constraints_between_tables
        CHECK(domainName IN SQL-Block)
    CONSTRAINTS table_constraints
        CHECK(domainName_A < domainName_B + 60)
 );
```

* A FOREIGN KEY in one table points to a PRIMARY KEY in another table. 外键必须是外表的主键
* CHECK-Clausel
  * Über Domain
  * Über Tabelle
  * Über mehre Tabellen

## 7.3 Datenbank Anfrage Sprache

1. FROM
   * **CROSS JOIN**
   * **NATURAL** [LEFT | RIGHT | FULL] **JOIN**
   * [LEFT | RIGHT | FULL] **JOIN ON()**
   * [LEFT | RIGHT | FULL] **JOIN USING()**
2. WHERE
   * \> | < | =
   * BETWEEN ... AND ...
   * LIKE
   * IS [NOT] NULL
   * IN | EXISTS | ANY / SOME | ALL
3. GROUP BY
4. HAVING
5. SELECT
   * ALL | DISTINCT
   * AS
   * Arithmetische Ausdrücke
   * Aggregatfunctionen
     * COUNT *(Null Value will be not counted)*
     * AVG
     * SUM
     * MAX
     * MIN
 6. ORDER BY *column_name ASC* | DESC

| EXISTS | Alternative |
| ------ | ----------- |
| WHERE     EXISTS(SELECT * FROM ...) | WHERE 0 < (SELECT COUNT(*) FROM ...) |
| WHERE NOT EXISTS(SELECT * FROM ...) | WHERE 0 = (SELECT COUNT(*) FROM ...) |

## 7.4 Daten Manipulation Sprache

#### INSERT

```sql
-- insert a item with only available values
INSERT INTO User(name)
VALUES(bob);

-- insert a item with all attribtte values
INSERT INTO User
VALUES(bob, P@ssw0rd);

-- insert a item with select items from other table
-- static value is also possible, e.g. P@ssw0rd
INSERT INTO User (
   SELECT name, 'P@ssw0rd'
   FROM Person
   WHERE name = bob);
```

#### UPDATE

```sql
UPDATE User
SET name = Bob
WHERE name = bob;
```

#### ALTER

```sql
ALTER TABLE table_name
ADD column_name column_definition

ALTER TABLE table_name
DROP column_name
```

#### DELETE

```sql
-- delete items from a table
DELETE FROM User
WHERE name = bob;

-- delete all items, empty table
DELETE FROM User;

-- delete a table
DROP TABLE User;
```

## 7.5 Daten Sichten

```sql
CREATE VIEW KundeKauftProdukttypen
  AS SELECT kundenName, kundenVorname, produktTyp
       FROM Kunden NATURAL JOIN Kauft NATURAL JOIN Produkt
      WHERE ort='Essen';
```

## 7.6 Daten Kontroll Sprache

## 7.7 Speicherung Struktur Definition Sprache

## 7.8 Datenschutz, Datensicherung und Datenkonsistenz

## 7.10 Charakteristika relationaler DBMS

## 8 Storage and Index structures, Query optimization

* Operationen-Baum
* Operationen-Optimierung

## 9.1 Concurrency Control / Transaktionsverfahren

* Probleme bei Parallelarbeit auf DB
  * **Lost Updates** R1 R2 W2 W1
  * **Dirty Read** R1 R2 W1
  * **Non-Repeatable Read** R1 R2 W1 R2
  * **Phantom Read** R1 INSERT_2 R1
* ACID Kriterium
  * Unteilbarkeit (atomicity)
  * Konsisitenz (consistency)
  * isolution (isolution)
  * Dauerhaftigkeit (durability)
* Abhängigkeitsgraph
  * Konflikt Bedingungen : at least a transaction want to write

## 9.2 Concurrency Control / Synchronisationsverfahren

* Sperrverfahren
  * **share lock** Lesesperre
    * several transactions could share read lock
  * **exclusive lock** Schreibsperre
    * a transaction can get exclusive lock only when no transaction has read lock on the traget object
* Fortgepflanztes Rollback
  * Problem : abgeschlossene Transaktionen müssen zurück gesetzt werden, im Widerspruch zum "durability"
* Zwei Phasen Sperr Protokoll
  * Wachstumsphase und Schrumpfungsphase
  * Variante
    * Einfache Zweiphasigkeit
    * Preclaiming
    * Strikte Zweiphasigkeit
    * Preclaiming und Strikte
* Deadlock
  * Gegenseitiger Ausschluss
  * Nichtentziehbarkeit
  * Warte und Halte-Fest
  * Mehrfachanforderung
* Auflösung von Deadlock
  * Prevention
  * Avoid
  * Time-out
  * Detection and Resolution
* Sperren über Prädikate
  * logische Sperren
  * besetigt das Problem von "Phantom Read"
* isolutionsstufen
  * **Read uncomitted** 共享锁忽略读写锁
  * **Read committed**  读锁在读取时上锁，写锁在整个事务期间上锁
  * **Repeatable Read** 读锁和写锁在整个事务期间上锁
  * **Serializable**

|                  | Dirty Read | Non-Repeatable Read | Lost Update | Phantom |
| ---------------- | ---------- | ------------------- | ----------- | ------- |
| Read uncommitted | Ja         | Ja                  | Ja          | Ja      |
| Read committed   | Nein       | Ja                  | Ja          | Ja      |
| Repeatable Read  | Nein       | Nein                | Nein        | Ja      |
| Serializable     | Nein       | Nein                | Nein        | Nein    |

## 9.3 Fehlertoleranz / Recovery

**Gegeben sein LOG** `<T, var, old_value, new_value>`
* **UNDO**
  * write old_value on disk
  * UNDO for all not finished transactions
* **REDO**
  * write new_value on disk
  * REDO for all finished transactions
* Recovery Policy
  * Not-Steal / Steal
  * Force / Not-Force
* ![](https://dl.dropboxusercontent.com/u/55616012/note/recovery.svg)

|           | steal      | not steal |
| --------- | ---------- | --------- |
| force     | UNDO       | -         |
| not force | REDO, UNDO | REDO      |
