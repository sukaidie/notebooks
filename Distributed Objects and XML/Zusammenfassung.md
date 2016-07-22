## 1. Grundlagen

#### Objektbasierte Systeme

* Objekt-basierte Sicht
* Der Zustand eines Objekts wird durch Primitive und die Zustände referenzierter Objekte dargestellt
* Klassen als Typbeschreibung von Objekten
* Datenkapselung

#### Primitive Datenstrukturen

* Variablen oder Konstanten
* Wert und Identifizierer
* Veränderung mittels Zuweisungen oder Manipulationen

#### Objekte

* Komposition : Einander referenzierende Objekte
* Kapselung
  * Schnittstelle definiert Bindung
  * Operationen
    * Integritätsbedingungen sicherstellen
    * erlaubte Wertebereiche einschränken

#### Klassen

* Kapselung
  * Zustandsraum
  * Verfügbare Services
  * Ausfall von Services
  * Interaktionen
* Attribute
* Operationen
  * In-Parametern *read only*
  * Out-Parametern *write only*
  * Inout-Parametern *read and write*
  * Typ des Rückgabewertes
  * mögliche Ausnahmen
* Vererbung

#### Komponenten

* Schnittstellen
  * Import (依赖)
  * Export (接口协议)
* Komposition
  * Benutzt-Beziehung: „A benutzt B“
  * Einbettung: „A bettet B ein“
  * Kommunikation: „A kommuniziert mit B über C“
* Parametrisierung (参数化，元数据配置)
  1. Ein- / Ausgabeparameter (类方法注解 @GET)
  2. Komponentenparameter (应用描述，依赖配置文件 web.xml, maven)
  3. Systemparameter (系统环境变量, Context)

#### Pakete

* Komponenten als Bausteine der Gesamtfunktionalität
* ejb, jar

#### Deployment

* Laufzeit-System (Servlet Container)
* Darstellung des Deployments
  * Deploymentartefakte

## 2. Sichten und Modelle

#### Grundlagen

* Anwendungszeitpunkte
  * Anforderungserhebung
  * Grob- und Feinentwurf
  * Implementierung
  * Validierung und Verifikation
  * Dokumentation für Nutzer

#### Modelltypen

* Komponenten und Schnittstellen : UML-Komponentendiagramm
* Abläufe : UML-Sequenzdiagramm
* Verteilung : UML-Verteilungsdiagramm
* Schichten
* Automaten : Zustandsautomat in UPPAAL
* Prozesse : Prozessmodellierung in Eclipse
* Datenmodelle : Entity-Relationship-Modelle
* Services

#### Klassifikation

* Statische Aspekte, Dynamische Aspekte
* Struktur, Verhalten

#### UML Diagramm

* Strukturdiagramme
  * Klassendiagramm
  * Objektdiagramm
  * Kompistionsdiagramm
  * Komponentendiagramm
  * Paketdiagramm
  * Verteilungsdiagramm
* Verhaltensdiagramme
  * Aktivitätsdiagramm
  * Zustandsdiagramm
  * Anwendungsfalldiagramm
  * Interaktiondiagramme
    * Kommunikationsdiagramm
    * Sequenzdiagramm
    * Timming-Diagramm
    * Interaktionsübersichtsdiagramm


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
* **Nebenläufigkeits-Transparenz:** Automatisches Serialisieren paralleler Anfragen
* **Replikations-Transparenz** mehrere Kopien eines Objektes
* **Fehler-Transparenz** Verstecken von Fehlerzuständen
* **Migrations-Transparenz** Objekte können an andere Orte bewegt werden
* **Leistungs-Transparenz"** Lastverteilung
* **Skalierbarkeits-Transparenz** funktionale Erweiterung
* Reference
  * 访问透明性：用相同的操作访问本地资源和远程资源。  
  * 位置透明性：不需要知道资源的物理或网络位置（例如，哪个建筑物或IP地址）就能够访问它们。  
  * 并发透明性：几个进程能并发地使用共享资源进行操作且互不干扰。  
  * 复制透明性：使用资源的多个实例提升可靠性和性能，而用户和应用程序员无须知道副本的相关信息。  
  * 故障透明性：屏蔽错误，不论是硬件组件故障还是软件组件故障，用户和应用程序都能够完成它们的任务。
  * 移动透明性：资源和客户能够在系统内移动而不会影响用户或程序的操作。  
  * 性能透明性：当负载变化时，系统能被重新配置以提高性能。  
  * 伸缩透明性：系统和应用能够进行扩展而不改变系统结构或应用算法。

## 4. Middleware

**Bewertung - Anforderungen**

| Middleware         | JAVA RMI       | CORBA          | Web Service    | REST           |
| ------------------ | -------------- | -------------- | -------------- | -------------- |
| Gemeinsame Nutzung | :+1:           | :+1:           | -              | :+1:           |
| Offenheit          | :ok_hand:      | :+1:           | :+1:           | :+1:           |
| Nebenläufigkeit    | :ok_hand:      | :ok_hand:      | -              | :shit:         |
| Skalierbarkeit     | :ok_hand:      | :ok_hand:      | -              | :+1:           |
| Fehlertoleranz     | :ok_hand:      | :ok_hand:      | -              | :shit:         |

**Bewertung - Transparenz**

| Middleware         | JAVA RMI       | CORBA          | Web Service    | REST           |
| ------------------ | -------------- | -------------- | -------------- | -------------- |
| Zugriff            | :+1:           | :+1:           | :ok_hand:      | :shit:         |
| Ort                | :ok_hand:      | :ok_hand:      | :ok_hand:      | :+1:           |
| Replikation        | :shit:         | :+1:           | :ok_hand:      | :shit:         |
| Migration          | :shit:         | :+1:           | :ok_hand:      | :shit:         |
| Leistung           | :shit:         | :+1:           | :ok_hand:      | :shit:         |
| Skalierbarkeit     | :shit:         | :+1:           | :ok_hand:      | :shit:         |
| Nebenläufigkeit    | :shit:         | :+1:           | :ok_hand:      | :shit:         |
| Fehler-Transparenz | :shit:         | :+1:           | :ok_hand:      | :shit:         |

:+1: Gegeben
:ok_hand: Beschränkt, abhängig von Plattform und Implementierung
:shit: Nicht Gegeben


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
* Prozedural
  * **RPC** Remote Procedure Call
    * Stubs
      * Automatisches Marshalling / Unmarshalling
      * bietet Typsicherheit und Synchronisation
    * Synchronisation und Typsicherheit
      * zwischen Server-Stub und Client-Stub
      * **IDL** Interface Definition Language
      * wird durch   **IDL** für Client und Server erreicht
    * Presentation Layer
      * Common Data Representaion (z.B. ASCII, UTF-8)
      * unterstützt Marshalling / Unmarshalling
    * Session Layer
      * Identifizierung von RPC-Servern
      * Aktivierung/Deaktivierung von RPC-Servern
      * Verteilung der Aufrufe an die richtige Stelle
* Obejekt-orientiert
  * OO-Middleware leist
    * IDL-Interface Design Language (z.B Java Interface, CORBA, WSDL)
    * Generierung von Client- & Server-Stubs
    * Session- & Presentation-Layer
  * Presentation Layer
    * Objektreferenz (复杂类型)
    * Ausnahmen und Behandelung (异常处理)
  * Session Layer
    * Objekte sind auf Unterschiedlichen Hosts
    * Objektreferenz > Objekt-Adapter (LocateRegistry) > Host > Remote Registry > Prozess > Objekt
  * Remote Server Prozess Registrierung (在客户端仓库内注册远程服务器服务信息)
  * Typsicherheit
    * Erweiterung einer Klasse
    * Implementierung eines Interfaces
* Nachrichten-orientiert

### 4.2 Java RMI

#### Remote Objects & Interfaces

Interface Definition Language in Java

```java
public interface Service extends Remote {
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
    public class Server implements Service { ... }
    Server server = new Server();
    Service service = (Service)UnicastRemoteObject.exportObject(server, 0);
    ```

  * Remote-Klasse erbt von UnicastRemoteObject

    ```java
    public class Server
    extends UnicastRemoteObject
    implements Service { ... }
    ```

* Pull to Registry

  ```java
  // Creates and exports a Registry instance on the local host
  // Accepts requests on the specified port.
  LocateRegistry.createRegistry(Registry.REGISTRY_PORT);
  // Returns a reference to the remote object Registry
  // on the specified host on the default registry port of 1099
  Registry r = LocateRegistry.getRegistry("10.0.0.1", "1099");
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
  Service service = (Service)registry.lookup("server");
  ```

* Entfernte Aufruf
  * Primitive Datentypen un d Objekt werden als Kopie übertragen
   (Pass by value)
  * Remote Objekte werden als entfernte Referenz übertragen
   (Pass by reference)

#### Remote Object Activation
####  Dynamisches Laden von Klassen

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

#### JSON

* Object ```{ [ "key" : value, "key" : value, ... }```
* Array  ```[ value, value, .... ]```
* Value ```string | number | Object | Array | boolean | null```

## 4.5  Web Services

* Architektur
  * ![](https://dl.dropboxusercontent.com/u/55616012/note/webservice.svg)
* Interface-Beschreibung (Registry)
  * **WSDL**: Webservice Description Language
  * Nachrichtenformat, Datentypen, Protocol, URL
* Verzeichnisdienste (Catelog)
  * **UDDI** Universal Description, Discovery and Integration
* Abwicklung des Aufrufs (Message)
  * **SOAP** Simple Object Access Protocol

```xml
<!--
String login(String login_request) { return login_response; }
Input Parameter of login()
-->
<message name="login_request">
   <part name="req" type="xs:string"/>
</message>
<!-- Return Parameter of login() -->
<message name="login_response">
   <part name="res" type="xs:string"/>
</message>
<!-- bining a port with Methode and messages -->
<portType name="login_port">
   <operation name="login">
     <input message="login_request"/>
     <output message="login_response"/>
   </operation>
</portType>
<!-- bining a port and relative SOAP Definition -->
<binding type="login_port" name="login_binding">
    <soap:binding style="document" transport="http://schemas.xmlsoap.org/soap/http"/>
    <operation>
      <input><soap:body use="literal"/></input>
      <output><soap:body use="literal"/></output>
   </operation>
</binding>
<!--publish a service to url-->
<service name="loginService">
  <port name="loginServerPort" binding="login_binding">
      <soap:address location="http://localhost/login"/>
  </port>
</service>

<!-- SOAP Message -->
<soapenv:Envelope>    
    <soapenv:Header/>
    <soapenv:Body>
        <loginService:getPersonByName>
          <login:arg_0>
            name
          </login:arg_0>
        </loginService:getPersonByName>
    </soapenv:Body>
</soapenv:Envelope>
```

## 4.6 REST

#### Konzepte

* Client-Server *通信只能由客户端单方面发起，表现为请求-响应的形式*
* Zustandslosigkeit *通信的会话状态（Session State）应该全部由客户端负责维护*
* Caching *响应内容可以在通信链的某处被缓存，以改善网络效率*
* Einheitliche Schnittstelle *统一接口*
  * Adressierbarkeit von Ressourcen  *Uniform Resource Locator (URL)*
  * Repräsentationen zur Veränderung von Ressourcen *HTML, JSON oder XML*
  * Selbstbeschreibende Nachrichten *HTTP Protocol*
  * Hypermedia as the Engine of Application State
* Mehrschichtige Systeme *每个组件只能访问与其交互的紧邻层，将架构分解为若干等级的层*
* Code on Demand (optional) *通过下载执行JS代码对客户端功能扩展*

#### Datenelemente

* **Resource**
* **Resource Identifier** URL
* **Representaion** JSOn or XML
* **Representaion Identifier** MIME type
* **Resource metadata**
* **Control data** GET / PUT / POST / DELETE

## 5 Komponentenbasierte Anwendungen

#### Application Server

* Komponentenausführung
  * Ausführungsumgebung für Komponenten
  * Verwaltung des Lebenszyklus von Komponenten
  * Kommunikation zwischen Komponenten
* Verteilung
  * Clientseitig ：GUI
  * Server ： Zentrale Dienste und Authentication
* Nutzung
  * Zugriff auf Komponenten
  * Kommerzielle Verwertung der Nutzung
* Skalierung
  * Server-Instanzen arbeiten auf verschiedenen physikalischen Maschinen
  * Last wird verteilt zwischen Maschinen

#### Container

* Konzept
  * Application Server führt Komponenten nicht direkt aus, sondern Container
  * Container können Komponenten zweckspezifisch verwalten
  * Nutzung von gemeinsamen Diensten des Application Servers
* Namensdienste 组件命名
* Metadaten 配置文件
* Pakete
  * Inhalt
    * Class and compiled library - JAR
    * Deployment Deskriptoren - WEB-INF
    * Statische Ressourcen - HTML, JSP, CSS, JPEG
  * Typen
    * compiled library - JAR
    * Web application - WAR
    * Enterprise Archive – EAR
      * JARs und WARs

#### Persistenz

* Mapping von Datenbank-Informationen auf Objekte
* Restriktionen für Attribute
* Enterprise Java Beans (EJB)

#### Geschäftslogik

* EJB Session Beans
* JDNI

#### Web / UI

* Generierung von Inhalten
  * Statisch, z.B. werden Bilder nur ausgeliefert
  * Vorlagenbasiert, z.B. HTML-Templates, die mit Inhalten befüllt werden
  * Programmcode, z.B. Behandlung spezieller Anfragen   
* Servlet
* Java Server Pages
  * Statisches HTML wird deklarativ geschrieben
  * Java-Code wird an gewünschter Stelle eingebettet (vgl. PHP)
  * Intern werden JSPs bei erster Ausführung zu Servlets kompiliert
