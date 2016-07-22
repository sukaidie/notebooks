## Aufgabe 1

1. **Erläutern Sie kurz (1) was fortgepflanzte Rollbacks sind, warum (2) diese problematisch sind und (3) unter welchen Umständen diese auftreten können.**
	1. Von einem fortgepflantztem Rollback spricht man, wenn der Abbruch einer Transaktion das Zurücksetzen von anderen Transaktion, von dieser Transaktion abhängig, möglicherweise bereits beendeten Transaktion zur Folge hat
	2. Möglicherweise bereits abgeschlosseTransaktionen müssen zurückgestzt werden, Widerspruch zum D Kriterium der ACID Eigenschaften
	3. Fortgepflantztes Rollback kann immer dann auftreten, falls Transaktion T1 von ihr geänderte Daten bereits von ihrem Ende freigibt werden, diese Daten von einer anderen Transaktion T2 genutzt, muss auch T2 zurückgesetzt werden, fall T1 scheitert
2. **Zeigen Sie, dass das strikte 2-Phasen Sperrprotokoll nicht deadlockfrei ist**
   * Siehe Blatt 09 Aufgabe 3b
3. **Nennen und erläutern Sie kurz die ACID-Kriterien**
   * A. Unteilbarkeit C. Konsistenz I. Isolation D. Dauerhaftigkeit
4. **Nennen Sie den Grund, warum es die Steal und Force-Policies gibt. Warum muss unter Verwendung von Steal/Force ein Undo, aber kein Redo durchgeführt werden?**
   * Verschiendene Politik wirken sich unterschiedlich auf Eigenschaften(Performenz, Fehlerbehandlung) des DBMS aus, je nach Anforderung kann die für diese Anforung passende Politik verwendet werden

## Aufgabe 2

R1(x) W2(z) R3(y) W1(y) R2(y) W2(y) W2(x) R1(y) R3(y)

| Operation | x    | y    | z |Wartlist                   |
|-----------|------|------|---|---------------------------|
|R1(x)      |S1R1U1|X1    |   |                           |
|W2(z)      |      |x     |   |W2(z)                      |
|R3(y)      |      |x     |   |W2(z)R3(y)                 |
|W1(y)      |W1    |      |   |W2(z) R3(y)                |
|R2(y)      |      |x     |   |W2(z) R3(y) R2(y)          |
|W2(y)      |      |x     |   |W2(z) R3(y) R2(y)W2(y)     |
|W2(x)      |      |x     |   |W2(z) R3(y) R2(y)W2(y)W2(x)|
|R1(y)      |      |R1U1  |   |W2(z) R3(y) R2(y)W2(y)W2(x)|
|W2(z)      |X2    |X2    |X2 |R3(y) R2(y)W2(y)W2(x)      |
|R2(y)      |      |W2U2  |   |R3(y) W2(x)                |
|R3(y)      |      |S3R3U3|   |W2(x)                      |
|W2(x)      |W2U2  |      |   |                           |
|R3(y)      |      |S3R3U3|   |-                          |

## Aufgabe 3 - Recovery & Synchronisation

1. Erläutern Sie die beiden folgenden Begriffe und erläutern Sie, welchen Einfluss sie auf das Recovery haben.
 * Transaktionskonsistenter Sicherungspunkt:
 * Aktionskonsistenter Sicherungspunkt:
2. Gegeben seien folgende Einträge in die Logdatei
 * keine Checkpoints, initiale Werte für X=10, Y=20 und Z=30)
 * `BOT T1, BOT T2, W1(X=1), W2(Z=3), BOT T3, W1(Y=2) COMMIT T1, W3(X=4) COMMIT T2, W3 (Y=5) --- Systemcrash ---`
 * Welche Aktionen müssen durchgeführt werden, wenn wir eine Steal/Not Force Policy unterstellen?
3. Erläutern sie kurz Prädikatsperren und nennen sie Gründe, warum sie zum Einsatz kommen.
