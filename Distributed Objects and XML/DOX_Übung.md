## Übungsblatt 1 – Komponenten

#### Aufgabe 1: Konzepte

Nennen Sie für die folgenden Konzepte die Umsetzung in Java:

1. Komposition
2. Klassen und Objekte - Class and Instanz
3. Operation - Method
4. Attribute
5. Gleichheit/Identität
6. In-Parameter einer Operation
7. Out-Parameter einer Operation
8. Inout-Parameter einer Operation
9. Typ des Rückgabewerts einer Operation
10. Schnittstelle - Interface
11. Komponente - Package

#### Aufgabe 2

1. Wird das Konzept der Kapselung in Java strikt umgesetzt? Geben Sie ein Beispiel bzw. ein Gegenbeispiel.
   * Nein, mittels getter()/setter()
2. Geben Sie Beispiele für die folgenden Arten von Parametern für eine Komponente:
   * Ein-Ausgabe-Parameter
   * Komponentenparameter
   * Systemparameter
3. Beschreiben Sie die Zusammenhänge der folgenden Begriffe: Klasse, Komponente, Paket, Deployment

## Übungsblatt 2 – Sichten und Modelle

#### Aufgabe 1: Theorie

1. Was versteht man unter einer Sicht auf ein System? Was ist der Vorteil der Verwendung von Sichten?
Aus welchem Grund existieren in der Regel mehrere Sichten auf dasselbe System?
2. Nennen Sie Ihnen bekannte Modelltypen zur geeigneten Darstellung folgender Aspekte
   * Komponenten und Schnittstellen
   * Verteilung von Komponenten
   * Zustände und Zustandswechsel
   * Prozesse
   * Daten
   * Interaktionen
   * Organisatorische Hierarchien
   * Zeit
   * Anforderungen
3. Worin unterscheiden sich statische und dynamische Aspekte eines Systems?
4. Zu welchen Zwecken werden Modelle im Model-Driven-Engineering eingesetzt? Welche Vorteil, aber auch welche Probleme ergeben sich daraus?

## Übungsblatt 3 – Verteilung

#### Aufgabe 1: Theorie

1. Geben Sie einige Beispiele für Ihnen bekannte verteilte Systeme.
2. Nennen Sie Eigenschaften verteilter Systeme.
   * Mehrere Komponenten auf mehreren Prozessoren
   * Gemeinsame Ressourcen
   * Ressourcen können ausfallen
   * Komponenten werden parallel ausgeführt
   * Komponenten können ausfallen
   * Mehr als ein Kontrollpunkt
   * Verteilung ist häufig durch nicht-funktionalen Anforderungen (Qualitäts-Anforderungen) getrieben
3. Welche Vor- und Nachteile haben verteilte Systeme?
4. Welche Anforderungen führen i. d. R. zu verteilten Systemen?
   * Gemeinsame Nutzung der Betriebsmittel
   * Offenheit
   * Nebenläufigkeit
   * Skalierbarkeit
   * Fehlertoleranz
5. Erläutern Sie die Transparenzen in verteilten Systemen und deren Beziehungen untereinander (Abbildung Folie 28 im Skript)

#### Aufgabe 2: Programm schreiben

```java
import java.io.*;
import java.net.Socket;

public class Main {

    public static final String HOST = "example.org";
    public static final int PORT = 80;

    public static void main(String[] args) throws IOException {
        Socket socket = new Socket(HOST, PORT);
        OutputStreamWriter streamWriter = new OutputStreamWriter(socket.getOutputStream());
        BufferedWriter bufferedWriter = new BufferedWriter(streamWriter);

        bufferedWriter.write("GET " + "/" + " HTTP/1.1\r\n");
        bufferedWriter.write("Host: " + HOST + "\r\n");
        bufferedWriter.write("\r\n");
        bufferedWriter.flush();

        BufferedInputStream streamReader = new BufferedInputStream(socket.getInputStream());
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(streamReader, "utf-8"));
        String line = null;
        while((line = bufferedReader.readLine())!= null)
        {
            System.out.println(line);
        }
        bufferedReader.close();
        bufferedWriter.close();
        socket.close();
    }
}
```

## Übungsblatt 4 – Middleware-Prinzipien

#### Aufgabe 1: Theorie

1. Wie werden entfernte Operationsaufrufe mit direkter Nutzung des Netzwerks implementiert?
   * Operationsaufrufe in einen Bitstring schreiben (serialisieren)
   * Operationsaufruf als Pakete über das Netz schicken
   * Auf die Antwort warten
   * Auf der anderen Seite empfangen, deserialisieren und interpretieren • Operationsaufruf ausführen
   * Antwort ebenso
2. Was sind die Nachteile der direkten Nutzung des Netzwerks ohne Middleware?
   * Manuelle Fehlerbehandelung
   * individuelle Protokoll definieren
   * Manuelle Abbildung von komplexen Strukturen auf Zeichenfolgen
   * Manuelle Auflösung von Heterogenität
   * Manuelle Implementierung der Komponenten-Aktivierung
   * Keine Typsicherheit (Zeichenfolgen)
   * Manuelle Synchronisation der beteiligten verteilten Komponenten
   * Keine Quality-of-Service-Garantien
3. Was sind die Aufgaben einer Middleware?
   * Erhöht die Verteilungstransparenz
   * Löst die Heterogenität
   * Erfüllt einige der generellen Anforderungen für verteilte Systeme
4. Wozu werden Stubs benötigt? Welche Aufgabe wird beim Marshalling/Unmarshalling durchgeführt?
   * Stubs leisten:
     * Client-Stub sendet die Aufforderung und wartet bis der Server fertig ist
     * Server Stub wartet auf die Aufforderung und ruft den Server auf, wenn die Aufforderungsdaten ankommen
   * Marshalling: Daten und Methodenaufruf für die Übertragung aufbereiten (Serialisieren)
   * Unmarshalling: Daten und Methodenaufruf aus der übertragenen Form wiederherstellen (Deserialisieren)
5. Wie wird durch den Einsatz von Middleware Zugriffstransparenz hergestellt?
   * Client-Stubs haben die gleichen Operation wie Server-Stubs
6. Wie wird durch den Einsatz von Middleware Ortstransparenz hergestellt?
   * Objekt-Identität
   * Objekt-Referenzen
   * Client-Aufrufe werden durch Objekt-Referenzen vermittelt
   * Keine Information im Client notwendig bezüglich des physischen Ortes
   * Problem: Wie kommt man an die Objekt-Referenzen?

## Übungsblatt 5 – RMI

#### Aufgabe 2: Theorie

1. Wozu wird eine IDL benötigt?
2. Begründen Sie die Reihenfolge des Vorgehens bei der Entwicklung mit einer OOMiddleware.
3. Nehmen Sie Stellung zu folgender Aussage: Der Einsatz einer Middleware macht die Berücksichtigung von Heterogenität im zu entwickelnden, verteilten System überflüssig.

## Übungsblatt 6 – RMI II

#### Aufgabe 1:

1. Welche Art der Kommunikation wird durch RMI ermöglicht?
   * RPC-Kommunikation zwischen JVMS
2. Auf welchen Ihnen bereits bekannten Grundlagen basiert RMI?
   * TPC Socket
   * Java Interface
3. Beschreiben Sie, wie ein Client einen Server auffinden kann, ohne seine Adresse zu kennen (Ortstransparenz).
   * `lookup("REGISTRY_NAME");`
   * anhand der IP-Address und dem entsprechenden Port
4. Beschreiben Sie die Grenzen von RMI.
   * Beschränkung auf Java-Welt
5. Warum sollte man bei der Implementatierung von „Remote Objects“ darauf achten, dass diese „Thread-safe“ ist?
   * Ein Remote Object wird möglichweise gleichzeitig von verschiedener entfernen Rechner aufgeruft, dabei gibs Concurrency Problems
6. Beschreiben Sie in wenigen Sätzen, wie Sie einen Client-Stub ohne RMI implementieren würden.

## Übungsblatt 7 – CORBA

#### Aufgabe 1: Theorie

1. Diskutieren Sie, wann der Einsatz welcher Middleware (CORBA, RMI) bzw. der Einsatz von Sockets (oder ähnlichem) in einem verteilten System sinnvoll ist.
2. Lässt sich der Namensraum bei Verwendung der CORBA IDL hierarchisch einteilen? Wenn ja, wie?
3. Welche Möglichkeiten bietet CORBA zur Definition von komplexen Typen? Was ist dabei einer Java Klasse am ähnlichsten?
4. Beschreiben sie ein mögliches Mapping für die in drittens genannten Konstrukte zu Java.

#### Aufgabe 2: CORBA IDL

* 2.2 CORBA-IDL I
```java
module Train {
  interface Train {
    // Ein Zug hat immer eine feste Anzahl von Sitzplätzen
    const short capabiliy;
    // nicht veränderliche Höchstgeschwindigkeit
    const short speed;
    // Des Weiteren wird für jeden Zug festgehalten, in welchem Zustand er sich befindet. Mögliche Zustände sind neu, gut, okay, schlecht
    enum status { neu, gut, okay, schlecht };  
  };
};
```

## Übungsblatt 8 CORBA und Datenrepräsentation

#### Aufgabe 1: CORBA Theorie

1. Beschreiben Sie ORB und IDL kurz. Nennen Sie vor allem den Einsatzzweck von ORB und IDL.
2. Welche Services bietet CORBA an?
3. Diskutieren Sie folgende Aussage: Alle Parametertypen aus der CORBA IDL können direkt in Java übernommen werden.
4. Bewerten Sie Corba anhand der Anforderungen an verteilte Systeme.

#### Aufgabe 2: Datenrepräsentation Theorie

1. Erklären Sie die Begriffe Interoperation und Interworking.
2. Nennen Sie Möglichkeiten (Sprachen), um Daten zu beschreiben.

## Übungsblatt 9 XML und JSON

#### Aufgabe 1: Theorie

1. Ordnen Sie die folgenden Begriffe einander zu und beschreiben Sie kurz, worum es sich dabei handelt: XML, SGML, DTD, XML Schema, DOM, JSON
2. Nennen und Beschreiben Sie die möglichen Ergebnisse einer XML-Validierung.
3. Wofür wird XSLT verwendet?
4. Wie können Referenzen in JSON-Dokumenten realisiert werden?
5. Nehmen Sie Stellung zu folgenden Aussagen:
   * XML ist in seiner Mächtigkeit durch fest definierte Tags beschränkt.
   * DTD ist eine Sprache zum Austausch von konkreten Daten, deren Struktur in XML beschrieben wurde.
   * XML ist eine weit verbreitet Grundlage für die Speicherung und den Austausch von Daten sowie vieler weiterer Anwendungsfälle?
   * JSON-Schema und XML-Schema werden mit der gleichen Syntax, welche durch die OMG standardisiert wurde, definiert.  
   * XML-Schema definiert die Sprachkonstrukte von XML

## Übungsblatt 10 WebServices

#### Aufgabe 1 :Theorie

1. Definieren Sie WebServices mit eigenen Worten.
2. Füllen Sie die Lücken im folgenden Diagramm:
   * ![](https://dl.dropboxusercontent.com/u/55616012/note/webservice.svg)
3. Beschreiben Sie die in 2. ergänzten Begriffe.
4. An welchen Stellen der WebService-Architektur spielt XML eine Rolle?
5. Damit Kosten gespart werden können, beschließt Ihr Projektmanager, dass eine bestimmte Funktionalität nicht selbst entwickelt werden soll, sondern externe Dienste in Form eines WebService verwendet werden. Beschreiben Sie, wie Sie vorgehen würden, wenn Sie diese Dienste in Ihre Java-Anwendung integrieren möchten.

## Übungsblatt 11 – REST und Komponentenbasierte Anwendungen

#### Aufgabe 1: REST

1. Beschreiben Sie die grundlegenden Konzepte von REST
2. Grenzen Sie die Begriffe Resource Identifier, Representation Identifier und Representation voneinander ab.
3. Vergleichen Sie das Konzept der RESTful Services mit WebServices. Welche Vorteile bietet REST?

#### Aufgabe 2: Komponentenbasierte Anwendungen

1. Was versteht man unter einem Application Server?
2. Was ist das Ziel von Application Servern?
3. Welches Konzept ermöglicht die (relativ) leichte Skalierung von Komponenten auf Application Servern?
4. Komponenten werden auf einem Application Server in Containern ausgeführt. Welche Aufgabe haben diese Container?
5. Welche Typen von Containern haben Sie im Rahmen der Veranstaltung kennengelernt?
6. Beschreiben Sie die in der Vorlesung vorgestellte Drei-Schichten-Architektur.
   * Welche Aufgabe hat die Persistenz-Schicht?
   * Welche Aufgabe hat die Geschäftslogik-Schicht?
   * Welche Aufgabe hat die Präsentations-Schicht (Web-Schicht)?
   * Auf welche Art kann die Web-Schicht Inhalte generieren? Nennen Sie entsprechende Techniken.
