## Aufgabe 1

Zeile 1. lost update
Zeile 2. Non-Repeatable Read
Zeile 3. Inkonsistente DB
Zeile 4. Phantom Problem

## Aufgabe 2

R4(x) R5(z) W5(z = z + 5) R2(z) W4(x = x \* 1,1) R1(x) R1(y) W1(x = x + 2) R3(x) W2(z = z + 3) W2(z = z \* 1,5) R3(y) W3(x = x \* 2) R3(z) W3(z = z - 1) W3(y = y - 5)

**a. Wie sähe die Logdatei für diesen Schedule unter logischer und physischer Protokollierung aus?**

| Zeitpunkt  | Operation   | Wert der Oper. | Eintrag(Phy.)   | Eintrag(Logi.)     |
|------------|-------------|----------------|-----------------|--------------------|
| 1          | BOT(T4)     | (10,15,20)     | (T4, BOT)       |                    |
| 2          | R4(x)       | (10,15,20)     |                 |                    |
| 3          | BOT(T5)     | (10,15,20)     | (T5, BOT)       |                    |
| 4          | R5(z)       | (10,15,20)     |                 |                    |
| 5          | W5(z=z+5)   | (10,15,25)     | (T5, z, 20, 25) | (T5, z, +, 5, -)   |
| 6          | COMMIT(T5)  | (10,15,25)     | (T5, COMMIT)    |                    |
| 7          | BOT(T2)     | (10,15,25)     | (T2, BOT)       |                    |
| 8          | R2(z)       | (10,15,25)     |                 |                    |
| 9          | W4(x=x*1,1) | (11,15,25)     | (T4, x, 10, 11) | (T4, x, *, 1.1, -) |
| 10         | COMMIT(T4)  | (11,15,25)     | (T4, COMMIT)    |                    |
| 11         | BOT(T1)     | (11,15,25)     | (T1, BOT)       |                    |
| 12         | R1(x)       | (11,15,25)     |                 |                    |
| 13         | R1(y)       | (11,15,25)     |                 |                    |
| 14         | W1(x=x+2)   | (13,15,25)     | (T1, x, 11, 13) | (T1, x, +, 2, -)   |
| 15         | COMMIT(T1)  | (13,15,25)     | (T1, COMMIT)    |                    |
| 16         | BOT(T3)     | (13,15,25)     | (T3, BOT)       |                    |
| 17         | R3(x)       | (13,15,25)     |                 |                    |
| 18         | W2(z=z+3)   | (13,15,28)     | (T2, z, 25, 28) | (T2, z, +, 3, -)   |
| 19         | W2(z=z*1,5) | (13,15,42)     | (T2, z, 28, 42) | (T2, z, *, 1.5, -) |
| 20         | COMMIT(T2)  | (13,15,42)     | (T2, COMMIT)    |                    |
| 21         | R3(y)       | (13,15,42)     |                 |                    |
| 22         | W3(x=x*2)   | (13,15,42)     | (T3, x, 13, 26) | (T3, z, *, 2, -)   |
| 23         | R3(z)       | (26,15,42)     |                 |                    |
| 24         | W3(z=z-1)   | (26,15,41)     | (T3, z, 42, 41) | (T3, z, -, 1, -)   |
| 25         | W3(y=y-5)   | (26,10,41)     | (T3, y, 15, 10) | (T3, y, -, 5, -)   |
| 26         | COMMIT(T3)  | (26,10,41)     | (T3, COMMIT)    | -                  |

**b. Die Transaktion 3 muss nach der Operation W3(z) zurückgesetzt werden. Es wird eine Steal-Politik angenommen**

UNDO, da eine Steal-Politik

| Zeitpunkt  | Operation       | Eintrag         |
|------------|-----------------|-----------------|
| 24         | (T3, z, 41, 42) | Z = 42          |
| 22         | (T3, x, 26, 13) | X = 13          |
| 16         | (T3, BOT)       | terminiert      |

**c. Kompensationstransaktionen**

T1  R1(x)W1(x=x-2)R1(y)
T2  R2(z)W2(z=z/1.5)W2(z=z-3)
T3  R3(y)W3(y=y+5)R3(z)W3(z=z+1)R3(x)W3(x=x/2)
T4  R4(x)W4(x=x/1.1)
T5  R5(z)W5(z=z-5)

**d. Recovery-Aktionen**

UNDO T3
Siehe Aufgabe 2 b)

REDO T1
Z15 (T1 COMMIT)

REDO T2
Z18 (T2,z,25,28) z=18
Z19 (T2,z,28,42) z=42
Z20 (T2,COMMIT) COMMIT T2
