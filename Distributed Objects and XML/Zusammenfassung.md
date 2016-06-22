## 3. Verteilung

#### Definition

* Ein verteiltes System ist eine Sammlung von autonomen Rechnern
* Diese Rechner sind durch ein Netzwerk verbunden
* Jeder Rechner führt Komponenten aus
* Diese Komponenten arbeiten auf der Basis einer (Verteilungs-)Middleware
* Die Middleware als Vermittlungsschicht lässt gegenüber dem Benutzer die Teile gemeinsam als ein einzelnes System erscheinen

#### Eigenschaften

* Mehrere Komponenten auf mehreren Prozessoren
* Gemeinsame Ressourcen
* Ressourcen können ausfallen
* Komponenten werden parallel ausgeführt
* Komponenten können ausfallen
* Mehr als ein Kontrollpunkt
* Verteilung ist häufig durch nicht-funktionalen Anforderungen (Qualitäts-Anforderungen) getrieben

#### Heterogenität

* Ebene
  * Hardware
  * Betriebssystem
  * Netzwerk
  * Programmiersprache
  * Datenpräsentation
  * Komponenten
  * Anwendungsplattformen
* Heterogenität auf Komponentenebene
  * Zu integrierende, existierende Komponenten oft Black Box
  * Kein Reengineering bzw. Modifikation möglich
* Integration  
  * Typische Lösung zur Integration externer Komponenten ist **Wrapping**
  * Erhöhung der Abstraktions-Ebene

#### Anforderungen an verteilte Systeme

* **Gemeinsame Nutzung der Betriebsmittel** *Daten im System gemeinsam zu benutzen*
  * Lösung: Resource-Manager
    * kontrollieren Zugriffsrechte
    * bieten Namensschemata
    * Kann zentral oder verteilt implementiert sein
* **Offenheit** *Erweiterbarkeit und Verbesserung eines verteilten Systems*
  * Schnittstellen müssen im Kontext des Systems öffentlich sein
  * Existierende Komponenten müssen ausgetauscht werden können
  * Integration neuer Komponenten muss möglich sein
  * Änderung des Systems muss zur Laufzeit möglich sein
  * Unterschiede in Darstellung und Präsentation müssen ausgeglichen werden
* **Nebenläufigkeit**
* **Skalierbarkeit** *von Performance*
  * Vergrößerung der Benutzerschaft
  * Einhaltung maximaler Antwortzeiten bei hoher Last
* **Fehlertoleranz** *Verbesserung der Zuverlässigkeit*
  * Recovery
  * Redundanz

#### Transparenz in verteilten Systemen

* **Zugriffs-Transparenz:** entfernte Komponenten verfügbar wie lokale
* **Orts-Transparenz:** Ortsunabhängiger Name
* **NebenläufigkeitsTransparenz:** Automatisches Serialisieren paralleler Anfragen  

## 4. Middleware

### 4.1 Prinzipien

#### Vernetzte Rechensysteme

* TCP und UDP
  | TCP | bidirektionaler Fluss  | Verbindungsorientiert |
  | --- | ---------------------- | --------------------- |
  | UDP | Unidirektionaler Fluss | Verbindungslos        |
* Wie gehen entfernte Operationsaufrufe?
  * Operationsaufrufe in einen Bitstring schreiben (serialisieren)
  * Operationsaufruf als Pakete über das Netz schicken
  * Auf die Antwort warten
  * Auf der anderen Seite empfangen, deserialisieren und interpretieren   
  * Operationsaufruf ausführen
  * Antwort ebenso
* Nachteile der direkten Benutzung des Netzwerks
  * Manuelle Abbildung von komplexen Strukturen auf Zeichenfolgen
  * Manuelle Auflösung von Heterogenität
  * Manuelle Implementierung der Komponenten-Aktivierung
  * Keine Typsicherheit (Zeichenfolgen)
  * Manuelle Synchronisation der beteiligten verteilten Komponente
  * Keine Quality-of-Service-Garantien

#### Middleware auf Verteilung

* Aufgaben
  * Schicht zwischen Netzwerk/Betriebssystem und der Anwendung
  * Erhöht die Verteilungstransparenz
  * Löst die Heterogenität
  * Erfüllt einige der generelen Anforderungen für verteilte Systeme
* **RPC** Remote Procedure Call
  * Stubs
    * Automatisches Marshalling / Unmarshalling
    * bietet Typsicherheit und Synchronisation
  * Synchronisation und Typsicherheit
    * zwischen Server-Stub und Client-Stub
    * **IDL** Interface Definition Language
    * wird durch **IDL** für Client und Server erreicht
  * Presentation Layer
    * Common Data Representaion (z.B. ASCII, UTF-8)
    * unterstützt Marshalling / Unmarshalling
  * Session Layer
    * Identifizierung von RPC-Servern
    * Aktivierung/Deaktivierung von RPC-Servern
    * Verteilung der Aufrufe an die richtige Stelle

### 4.2 Java RMI

#### Remote Objects & Interfaces

Interface Definition Language in Java
```java
public interface Serviece extends Remote {
    String getName() throws RemoteException;
};
```
**Server Stub**
* Hat die folgenden Aufgaben:
  1. Unmarshalling des entfernten Aufrufs und der Parameter
  2. Aufruf der gewünschten Methode in dem Zielobjekt
  3. Marshalling des Ergebnisses
* Einen Server-Stub erstellen
  * UnicastRemoteObject.exportObject nutzen
    ```java
    public class Server implements Serviece { ... }
    Server server = new Server();
    Serviece s = (Serviece)UnicastRemoteObject.exportObject(s, 0);
    ```
  * Remote-Klasse erbt von UnicastRemoteObject
    ```java
    public class Server
    extends UnicastRemoteObject
    implements Serviece {  ... }
    ```
* Pull to Registry
  ```java
  // Erstellen einer Registry
  LocateRegistry.createRegistry(Registry.REGISTRY_PORT);
  // Holen einer existierenden Registry
  Registry r = LocateRegistry.getRegistry("10.0.0.1");
  // Methoden von Registry:
  // Binden
  r.bind("ServieceName", o);
  // Objektreferenz nach Namen finden
  r.lookup("ServieceName");
  // Liste von Objektreferenzen holen
  r.list();
  //Bindung lösen
  r.unbind("ServieceName");  
  ```
**Client-Stub**
 * Hat die folgenden Aufgaben:
   1. Erstellen einer Verbindung zur entfernten JVM
   2. Marshalling des Remote-Aufrufs inkl. Parametern
   3. Synchronisation sicherstellen (auf Antwort warten)
   4. Unmarshalling des Ergebnisses oder der Exception
   5. Ergebnis (oder Exception) an Aufrufenden weiterleiten
 * Einen Client-Stub bekommen
   ```java
   Serviece serviece = (Serviece)registry.lookup("server");
   ```
 * Entfernte Aufruf
   * Primitive Datentypen und Objekt werden als Kopie übertragen
     (Pass by value)
   * Remote Objekte werden als entfernte Referenz übertragen
     (Pass by reference)
#### Remote Object Activation
#### Dynamisches Laden von Klassen

## 4.3 CORBA

## 4.4 XML und JSON

#### Heterogene Middleware
  * **Interoperation** *The ability of two systems to perform a given task using a single set of rules*
  * **Interworking** *The ability of two systems to perform a given task that each systems implements a different set of rules*

#### XML

* Aufbau
  * Strukturdefinition
    * Document Type Definition (DTD)
    * XML Schema
  * Daten *Document Object Model (DOM)*
    * Dynamischen Zugriff auf Inhalt, Struktur und Layout
* Parsen
  * DOM-Parser : *Hierarchische Baumstruktur*
  * SAX-Parse : *Zugriff auf einzelne Inhalte durch Events (Push)*
  * StAX-Parser : *Dokumententeile als Datenstrom (pull)*
* Inhalte
  * **DTD** Document Type Definition
    * Grundelemente:
      * Documenttypen `<!DOCTYPE html>`
      * Elementtypen `<!ELEMENT body (#PCDATA)>`
      * Attributlisten `<!ATTLIST person id ID #REQUIRED>`
      * Entitäten
      * Notationen
  * **Element** has Attributes and Text
    ```html
    <Element id="Attribute">Text</Element>
    ```
  * Process Instraction
    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    ```
  * **Name Space** *xmlns, z.B. wsd, soap, html, android*

    ```xml
    <config xmlns:rnc="RES_URI">
      <rnc:node>Plant text</rnc:node>
    </config>
    ```
  * Element Type
    * Root *unique, not null*
    * Child
    * Empty `<EmptyElement/>`
  * Linking
    * X-Path
    * X-Pointer

## 4.5  Web Services

#### Architektur
* Interface-Beschreibung (Registry)
  * **WSDL**: Webservice Description Language
* Verzeichnisdienste (Catelog)
  * **UDDI** Universal Description, Discovery and Integration
* Abwicklung des Aufrufs (Message)
  * **SOAP** Simple Object Access Protocol
