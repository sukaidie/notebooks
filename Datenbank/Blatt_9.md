## Aufgabe 1

a. **R3(y) R1(x) W3(z) R2(z) W3(y) R4(y) R1(y) W1(x) W4(x) R2(y) R5(z) W2(z)**
   * R1(x) W1(x) W4(x)
     * 1 > 4
   * R3(y) W3(y) R4(y) R1(y) R2(y)
     * 3 > 4, 3 > 1, 3 > 2
   * W3(z) R2(z) R5(z) W2(z)
     * 3 > 2, 3 > 5, 5 > 2

b. **R4(y) R4(x) R1(x) R1(y) R3(y) R2(z) W4(x) W1(x) R2(y) W2(z) W3(z) R5(z) W3(y) W5(z)**
   * R4(x) R1(x) W4(x) W1(x)
     * 1 > 4, 4 > 1
   * R4(y) R1(y) R3(y) R2(y) W3(y)
     * 4 > 3, 1 > 3, 2 > 3
   * R2(z) W2(z) W3(z) R5(z) W5(z)
     * 2 > 3, 2 > 5, 3 > 5

![](https://dl.dropboxusercontent.com/u/55616012/note/dbms_concurrency.svg)

## Aufgabe 2

**R4(y) R5(z) R1(x) R3(y) W3(z) W5(z) W3(y) R2(z) W4(x) R1(y) W1(x) R2(y) W2(z)**

* R1(x) R1(y) W1(x)
* R2(z) R2(y) W2(z)
* R3(y) W3(z) w3(y)
* R4(y) W4(x)
* R5(z) W5(z)

**Striktes ZweiphasenSperrprotokoll**
* R4(y) R5(z) R1(x) R3(y) W5(z) W3(z) R1(y) W1(x) W4(x) W3(y) R2(z) R2(y) W2(z)

**Zweiphasen-Sperrprotokoll mit Preclaiming**

* R4(y) R5(z) W5(z) R3(y) W3(z) W3(y) R2(z) W4(x) R1(x) R1(y) W1(x) R(y) W2(Z)

## Aufgabe 3

* a. Gegenseitger Abschluss, Nichtentziehbarkeit, Warte-und-Halte-Fest, Mehrfaceanforderung
* b. R1(y) R1(x) R2(x) R2(y) W2(y) W1(x) W1(y) W2(x)
