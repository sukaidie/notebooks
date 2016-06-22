
## 2.0 Data Model and Types

* ER Diagramm
  * **1:1, 1:N, N:M**
  * Martin Notation

![]( https://upload.wikimedia.org/wikipedia/commons/thumb/0/0d/ERD_Darstellungen.png/300px-ERD_Darstellungen.png)

## 3.0 Ableitung eines Schemas aus ER-Diagramm

* Glossar
  * Klassfikation : 分类
  * Assoziation : 关联
  * Aggregation : 聚合
  * Composition : 合成
  * Generalisierung
* 1: N : write 1 to N as Foreign Key
* N: M : muss dazu eine Tabelle erstellt werden

## 4.0 Normalformen

1. 1NF： 数据库表的每一列都是不可分割的基本数据项
Attribtte should be automar.
2. 2NF : 普通键依赖全部候选键，即一组候选（主）键构成超键可以标示唯一实例
it does not exist functional dependencies between normal keys and candidate keys.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/0/0f/PrimaryKey_zht.svg/280px-PrimaryKey_zht.svg.png)
3. 3NF ： 普通键之间没有函数关系
it does not exist functional dependencies between normal keys.

## 6.5 Relationale Algebra

1. **Kartesisches Produkt** $\times$
 * kommutativ
 * assoziativ
 * ( CROSS ) JOIN 的顺序及优先级不影响结果表
2. **Vereinigung** $\cup$
3. **Differenz** EXCEPT
4. **Durchschnitt** INTERSECT
5. **Selektion** $\sigma$
6. **Projektion** $\pi$
7. **Division**
8. **(Innerer) Verbund** $\bowtie$
 * Kombination aus Kartesischem Produkt, Selektion nach Verbundbedingungen
 * kommutativ und assoziativ
 * **Thetaverbund** $\bowtie_\theta$
 * **Gleichverbund** $\bowtie_=$
9. **Natürlicher Verbund**
10. **Semiverbund**

![](https://dl.dropboxusercontent.com/u/55616012/note/Verbund.png)

## 7.2 Datendefinitionsprache

![](https://db.tt/RgoxNMlK)

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
(TIME'09:00:00', INTERVAL'-50' MINUTE) OVERLAPS (TIME'02:15:00', INTERVAL'6' HOUR
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

* 外键必须是外表的主键
* CHECK-Clausel
 * Über Domain
 * Über Tabelle
 * Über mehre Tabellen

## 7.3 Datenbank Anfrage Sprache

* SELECT
 * ALL | DISTINCT
 * AS
 * Arithmetische Ausdrücke
 * Aggregatfunctionen
   * COUNT *(Null Value will be not counted)*
   * AVG
   * SUM
   * MAX
   * MIN
* FROM
 * **CROSS JOIN**
 * **NATURAL** [LEFT | RIGHT | FULL] **JOIN**
 * [LEFT | RIGHT | FULL] **JOIN ON()**
 * [LEFT | RIGHT | FULL] **JOIN USING()**
* WHERE
 * Vergleichsprädikate
 * Nullmarken
 * Nullmarken in Boolschen Ausdrücken
 * GROUP BY
 * HAVING
 * IN | EXISTS | ANY / SOME | ALL

| EXISTS | Alternative |
| ------ | ----------- |
| WHERE EXISTS(SELECT * FROM ...) | WHERE 0 < (SELECT COUNT(*) FROM ...) |
| WHERE EXISTS(SELECT * FROM ...) | WHERE 0 = (SELECT COUNT(*) FROM ...) |

## 7.4 Daten Manipulation Sprache

## 7.5 Daten Sichten

## 7.6 Daten Kontroll Sprache

## 7.7 Speicherung Struktur Definition Sprache

## 7.8 Datenschutz, Datensicherung und Datenkonsistenz

## 7.10 Charakteristika relationaler DBMS

## 8 Storage and Index structures, Query optimization

## 9.1 Concurrency Control / Transaktionsverfahren

## 9.2 Concurrency Control / Synchronisationsverfahren

## 9.3 Fehlertoleranz / Recovery
