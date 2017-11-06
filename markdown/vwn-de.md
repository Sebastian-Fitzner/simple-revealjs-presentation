# Volkswagen Nutzfahrzeuge

### A short technical overview

--

## Sitemap

--

## Let's talk about ... (10:00 min)
1. Client & Requirements
1. History
    1. The New Amarok 2.0
    1. The New Crafter 2.0
    1. Spirit of Amarok

--

## Projects in 2017
1. Drupal - a new problem is born
1. GlobeSwift als Lösung
1. Projekte
    - The New Crafter 4.0
    - Bulli 70 Jahre

--

## Technical Deep Dive (30:00 min)

1. General Workflow (3:00 min)
    - Git
    - Jenkins
1. Frontend (4:00 min)
    - Building Blocks
    - Veams
1. Backend (10:00 min)
    - NodeJS
    - Express
    - Mangony
1. Api (10:00 min)
    - TCT (09/2016)
    - Drupal (01/2017)
    - GlobeSwift (04/2017)

---

# Let's talk about ...

--

## Kundenanforderungen

Ganz allgemein gesprochen ist die Anforderung sehr konkret und speziell.

Es gibt **Landing Pages**, die folgendes unterstützen müssen:

--

### Jede Landing Page soll auch mehrere Seiten beinhalten können (Home, Products etc.).
#### _(laangweilig)_


--

### Jede Landing Page soll im Inhalt übersetzt werden können (inkl. Bilder)
#### _(Nichts neues)_

--

### Jede Übersetzung einer Landing Page kann eine andere Reihenfolge und die Sichtbarkeit der Elemente steuern.
#### _(Hmm, wir brauchen ein Formular um diese Daten zu speichern - pfff)_

--

### Jede Übersetzung einer Landing Page can unabhängig mit anderen UI Elementen (Slider, Accordion etc.) veröffentlicht werden.
#### _(what?!)_

--

### Jede Übersetzung einer Landing Page kann in einem Preview Mode angeschaut werden. Das soll einfach über Parameter in der URL funktionieren.

Dies beinhaltet ebenfalls verschiedene Versionen (Inhalte, UI Elemente, Seiten), heißt man kann komplett in Versionen wechseln indem man einen einzigen Parameter in der URL nutzt.


![alt OH](assets/img/oh-man.gif "oh man")

#### _(Kein Problem ...)_

--

## History

Dafür gibt es das TCT von VW. Es unterstützt fast alles davon, wenn man etwas um die Ecke denkt und Hirnschmalz reinbuttert.

Also entschieden wir uns, das Folgende zu tun:

--

### Löschen des Legacy Codes, der in PHP geschrieben wurde.

Dieser war mit CodeIgniter 2 geschrieben und konnte die oben genannte Anforderungen nicht erfüllen.

--

### Erstellen eines eigenen Frameworks in NodeJS

Wir wollten uns hier das Leben erleichtern und die ganzen Frontend Templates gleichzeitig im Backend benutzen.
--

### Überdenken der allgemeinen XML-Struktur, welche wir dann ins TCT hochladen

- Anstelle von einer Datei pro Landing Page wurden es zwei (Settings, "Alles andere")
- Erstellen einer neuen "Alles andere" Version für jede Major Version der Landing Page

--

### Verbinden des NodeJS Frameworks mit dem TCT

--

### Fallback-Verhalten in NodeJS Framework

So mussten wir auf die PHP-Applikation verweisen, wenn die Version noch eine Alte ist.

--

### Erstellen von automatisierten Tasks um die XML-Datei für das TCT zu generieren

--

### Unterstützung einer lokalen XML-Datei für Entwicklungs-Pozess

Man will ja nicht immer ins TCT gehen und jede Änderung hochladen.

--

Mit diesen Hintergrund schauen wir uns das Ergebnis von 01/2017 an.

--

1. [The New Amarok 2.0](http://the-new-amarok.com/de/de/home.html)
1. [The New Crafter 2.0](http://the-new-crafter.com/pl/pl/home.html)
1. [Spirit of Amarok](http://www.spirit-of-amarok.de/de/de/home.html)

---

# Projekte in 2017

--

2017 haben wir dann mit der zweiten Phase von "The New Crafter" begonnen. Durch die wachsenden Anforderungen (Anzahl der Unterseiten steigt)
haben wir die Implementierung eines CMS verkauft, weil das TCT zu große Datensätze produzierte.

--

## Drupal - ein neues Problem ist gebohren

![alt Doomed](assets/img/doomed.gif "Doomed")

_Das Monster im Hintergrund ist Drupal :(_

--

## Eine kurze Zusammenfassung der Probleme

- Übersetzung von Inhalten passiert feld-basiert.
- Revisions-Hölle
- Content Moderation (Draft und Publish) in Verbindung mit Übersetzungen war nicht leicht zu handhaben (eigentlich gar nicht)
- Dynamisches Zusammenstellen des Inhalts via Paragraphs (ein Modul) führte zu deutlichen Performance-Schwierigkeiten im Backend und im API-Call

--

![alt Rock](assets/img/solution-rock.gif "Rock")

--

## GlobeSwift als Lösung

Am Ende führte dies zu einen 3-Wochen-Sprint, in dem wir zu zweit ein neues Tool erstellten, das all diese Probleme löste und ein kompletter Ersatz des TCT darstellt.

![alt solution](assets/img/solution.gif "solution")

--

## Projekte

- [The New Crafter 4.0](http://the-new-crafter.com/de/de/home.html)
- [Bulli 70 Jahre](https://www.70jahrebulli.de/de/de/home.html)

---

# Technischer Deep Dive

---

## Allgemeiner Workflow

--

- Versionierung erfolgt über Git
    - [Git Projects](https://gitlab.aperto.de/VWN)
    - [Git BB](https://gitlab.aperto.de/VWN-BB)
- Wir nutzen Gitflow
- Wir nutzen Jenkins um zu deployen
    - [Jenkins](https://phpbuild.aperto.de/view/VWN/)
- Wir nutzen mehrere Instanzen (dev, qa-intern, qa-extern, live)

--

### Frontend
#### Veams

Mit Hilfe von Veams haben wir schließlich eine Building-Blocks-Bibliothek geschrieben:
- [Building Blocks](http://demo.aperto.de/presentation/vw-building-blocks/develop/)

--

### Backend
- NodeJS
- Express
- Mangony

--

## Api
- [TCT (09/2016)](http://tct.volkswagen.com/cvtct/protected/start.html)
- [Drupal (01/2017)](https://vwn.live.aperto.de/welcome)
- [GlobeSwift in Drupal (04/2017)](http://vwn-cms.dev.aperto.de/poolswift#/?_k=yrncnh)

---

## Infrastruktur

--

### Wie funktioniert das nun?

1. Alle Requests werden von dem Apache aufgefangen.
1. Es gibt im Apache einen Reverse Proxy zur NodeJS-Applikation.
1. Das NodeJS-Framework kommuniziert nun das erste Mal mit der TCT-Api und holt sich die settings.xml in dem die Version des Webspecials gespeichert ist.
    1. Wenn die Einstellung auf eine alte Version verweist, findet ein nächster Reverse Proxy statt, der auf die PHP-Applikation verweist.
    1. Bei einer neuen Version wird das Framework komplett den Request verarbeiten und den Inhalt vom TCT holen und darstellen.

--

<img src="assets/img/VWN-LP_Infrastructure.jpg" width="600px" height="auto" />

--

### Vorteile

- Der alte PHP-Code bleibt unverändert.
- Updates werden nur in ihrer Version angewendet
- Layouts können weiterentwickelt werden, nur das Datenobjekt ist für die individuelle Darstellung der Landing Page verantwortlich

--

### Jenkins

Jenkins ist unsere Deployment- und Build-Software. Alle Jobs wurden von uns erstellt und beinhalten:

- Dev-, QA-Intern-, QA-Extern-Jobs
- Feature-Builds

---

## Setup

--

Wir haben 3 Haupt-ELemente in jedem Projekt:

- NodeJS Framework
- Webspecial-Version
- Building Blocks

Diese Elemente sind jeweils ein separates Git-Repository. Zusätzlich dazu ist jedes UI-Element ebenfalls ein Git-Repository.

--

<img src="assets/img/VWN-Project-Diagram1.jpg" width="1200px" height="auto" />

--

<img src="assets/img/VWN-Website-Structure.jpg" width="1200px" height="auto" />

---

## NodeJS Framework

1. Das Framework ist das Haupt-Repo und inkludiert alle anderen Repositories als Git-Submodule.
1. Das Framework ist eine ExpressJS Node Applikation

--

### Verantwortlichkeiten

- Server starten
- Kommunikation mit den APIs
- Behandlung von Requests und Proxy
- Seitendarstellung via Mangony Renderer und Data Handler

---

## Webspecial

1. ... beinhaltet die allgemeine Building-Blocks-Bibliothek (Layout, allgemeine Styles etc.)
1. ... beinhaltet eine definierte Version von bestimmten UI Elementen
1. ... beinhaltet entweder XML für das TCT oder JSON-Schema-Dateien für GlobeSwift
1. ... beinhaltet das Theming für das Webspecial

--

<img src="assets/img/VWN-Webspecial.png" width="1400px" height="auto" />

--

### TCT

Beim Einsetzen von TCT pflegen wir eine content.xml mit Hilfe von Includes und dies wird dann automatisiert via Grunt gebaut.

--

### GlobeSwift

Bei der Nutzung von GlobeSwift generieren wir automatisch unsere JSON-Schema-Formulare indem wir Mangony benutzen.

---

## Building Blocks

1. ... besteht zum Einen aus einen allgemeinen Teil
1. ... besteht zum Anderen aus diversen Git-Submodulen, die schließlich als UI-Elemente genutzt werden können

--

<img src="assets/img/VW-Building-Blocks.png" width="1400px" height="auto" />

--

### Allgemeine Struktur

- Alle Building Blocks sind self-contained
- Alle Building Blocks haben dieselbe Ordner- und Datei-Struktur
``` bash
.
├── ./INSERTPOINTS.md
├── ./README.md
├── ./c-gallery.hbs
├── ./c-gallery__item.hbs
├── ./c-gallery__slider-item.hbs
├── ./gallery-bp.hjson
├── ./gallery.schema.hbschema
├── ./gallery.ui-schema.hbschema
├── ./js
│   └── ./js/gallery.js
└── ./scss
    └── ./scss/_c-gallery.scss
```
- Kombinationen werden von außen nach innen benannt (`slider-teaser.hbs`)

---

## Fragen?

![alt Questions](assets/img/questions-bale.gif "Questions")

--

## Ende im Gelände