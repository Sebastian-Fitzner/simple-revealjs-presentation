# Volkswagen Nutzfahrzeuge

### A short technical overview

--

## Sitemap

--

## Let's talk about ... (10:00 min)
1. Client & Requirements
1. History
    1. Spirit of Amarok 2.0
    1. The New Crafter 2.0
    1. Spirit of Amarok

--

## Projects in 2017
1. Drupal - a new problem is born
1. Poolswift as Solution
1. Projects
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
    - Poolswift (04/2017)

---

# Let's talk about ...

--

## Client & Requirements

In general the whole setup is really special.
There are **landing pages** which have the following requirements:

--

### Every landing page can contain multiple pages
#### _(boring)_


--

### Every landing page can have a translation and other images
#### _(well, nothing new)_

--

### Every translation of a landing page can have a different sort order and/or visibility of elements
#### _(hmm, we need a form to save this data - pfff)_

--

### Every translation of a landing page can be published independently in another building blocks version
#### _(what?!)_

--

### Every translation of a landing page can be reviewed in a preview mode by using parameters.
This also contains different versions, means you can switch versions and content by using one single parameter.

#### _(I don't see any problems ...)_

![alt OH](assets/img/oh-man.gif "oh man")

--

## History

That's why there is the TCT of VW. It supports almost everything of that by adding a bit of brainpower ...

So we decided to do the following:

--

### Forget about the legacy stuff written in PHP

--

### Create our own framework in NodeJS

--

### Rethink general XML structure which we upload to the TCT by:

- creating two projects for one landing page (one for "settings", the other "everything else")
- creating a new "everything else" version for every major version of the landing page

--

### Connect the TCT with our custom framework

--

### Have a fallback handling in our framework

--

### Re-use the frontend templates in the backend

--

### Create automation tasks to generate files for the TCT

--

### Have local versions running for development process

--

With that in mind, let's see what we achieved til end of 01/2017.

--

1. [The New Amarok 2.0](http://the-new-amarok.com/de/de/home.html)
1. [The New Crafter 2.0](http://the-new-crafter.com/it/it/home.html)
1. [Spirit of Amarok](http://www.spirit-of-amarok.de/de/de/home.html)

---

# Projects in 2017

--

## Drupal - a new problem is born

In 2016 we sold Drupal to solve the scalibity problems in TCT. Well ...

![alt Doomed](assets/img/doomed.gif "Doomed")

_The monster in the background is Drupal and we are the little, innocent kid in front of it :(_

--

## Short summary of problems

- Translation of content is field based
- Revision hell
- Draft & publish states aren't easy to handle (not at all)
- Dynamically build your content with paragraphs leads to a lot of performance issues

--

So, we escalated this a lot of times ...

![alt Rock](assets/img/solution-rock.gif "Rock")

--

## Poolswift as Solution

In the end it leads to a 3-week-sprint in which we had to create a new tool which solves all the problems and is a real replacement of the TCT.

![alt solution](assets/img/solution.gif "solution")

--

## Projects (in progress)

- [The New Crafter 4.0](http://vwnlp-crafter.qa.aperto.de/de/de/home.html?preview=true)
- [Bulli 70 Jahre](https://www.70jahrebulli.de/de/de/home.html)

--

So let's see the technical stuff in detail.

---

## General Workflow (3:00 min)

- [Git Projects](https://gitlab.aperto.de/VWN)
- [Git BB](https://gitlab.aperto.de/VWN-BB)
- [Jenkins](https://phpbuild.aperto.de/view/VWN/)

--

## Frontend (4:00 min)
- [Building Blocks](http://demo.aperto.de/presentation/vw-building-blocks/develop/)
- Veams

--

## Backend (13:00 min)
- NodeJS
- Express
- Mangony

--

## Api (13:00 min)
- [TCT (09/2016)](http://tct.volkswagen.com/cvtct/protected/start.html)
- [Drupal (01/2017)](https://vwn.live.aperto.de/welcome)
- [Poolswift (04/2017)](http://vwn-cms.dev.aperto.de/poolswift#/?_k=yrncnh)