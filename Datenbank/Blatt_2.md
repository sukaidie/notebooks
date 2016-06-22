**Datenbanksystem** | Übungsblatt 02

### **Aufgabe 01**

Ein Professor kann mehrere Lehrveranstaltungen abhalten, wobei eine Lehrveranstaltung immer einem Professor zugeordnet sein muss.

**Professor** ( professorID , name)
**Lehrveranstaltungen** ( lvID , raumID , professorID )


Zusätzlich können die Lehrveranstaltungen von Mitarbeitern unterstützt werden.
Mitarbeiter unterstützen Lehrveranstaltungen in unterschiedlicher Art und Weise (z.B. als "Hauptansprechpartner", als "Übungsgruppenkoordinator" oder als "Übungsserveradministrator").

**Unterstützung** ( id , mitarbeiterID , art )

Studenten besuchen Lehrveranstaltungen und Übungsgruppen.

**Student** ( martikelNr , name )
**StudentUebung** ( martikelNr , gruppID )

Außerdem können zu einer Lehrveranstaltung Übungsgruppen angeboten werden. Übungsgruppen können ohne eine zugeordnete LV nicht existieren.

**Uebung** ( uebungID , raumID , lvID )

Die Übungsgruppen werden von einem Mitarbeiter betreut. Jeder Mitarbeiter kann mehrere Übungsgruppen leiten.

**Uebungsgrupp** ( gruppID , lvID , raumID , mitarbeiterID )
**Mitarbeiter** ( mitarbeiterID , raumID )

Die Räume werden in Büros und Veranstaltungsräume unterteilt. Ein Veranstaltungsraum kann nicht gleichzeitig ein Büro sein.
Die Lehrveranstaltung und die Übungsgruppen sind Veranstaltungsräumen zugeordnet.
Professoren haben ein eigenes Büro während es Mitarbeiter gibt, die sich ein Büro mit anderen Mitarbeitern teilen müssen.

**Raum** ( raumID )
**Buero** ( raumID , professorID )
**VeranstaltungsRaum** ( raumID )


###  Aufgabe 02


![](https://dl.dropboxusercontent.com/u/55616012/note/ERP.png)
