# Veams Workshop

---

## Sitemap

1. What is the workshop about?
2. Veams-Cli - Project Setup
3. Veams-Cli - Components
4. Veams-Cli - Blueprints
5. Veams Framework
6. Veams in Practice

---

## What is the workshop (not) about?

--

### (It is not about)
#### Templating

Mangony is responsible for:
- Data Handling
- Templating
    - Partials
    - Pages
    - Layouts
- Handlebars Helpers

http://mangony.veams.org/

--

### (It is not about)
#### Tasks Runner Configuration

After scaffolding a project the developers are responsible for re-configuring the tasks.

--

### Veams-Cli and Scaffolding

To scaffold a project or blueprints like components you can use `veams-cli`.

See https://www.npmjs.com/package/veams-cli for an overview.

--

### Veams with JS/SCSS

To work with JavaScript and SCSS you have to use Veams.

The current version is v5.xx and you can find the documentation at https://github.com/Veams/veams.

---

## Veams-Cli

--

### Introduction

In general we refactored the whole cli and generators in there.
Currently we work on making the package stable, that's why it is now in `alpha` state.

--

We decided to go away from plugin based prompts and rewrote that stuff to subject based prompts.

--

Furthermore we want to support project types as a new choice for you, means we can distinguish between:
 - static-page-app
 - single-page-app (with React)

--

### Installation of Veams-Cli

Install veams-cli globally by executing `npm i -g veams-cli/@next`.

--

### Setup a Project with Veams-Cli

Creating a new project is very simple. Make sure you already have created a testing folder like `my-custom-project`.

Just execute the following line in that folder:

``` bash
veams new project
```

--

### Folder structure

That's what the folder structure should look like after scaffolding a new project ...

``` bash
 ├── app
 │   ├── ...
 ├── configs
 │   ├── ...
 ├── server
 │   ├── ...
 └── src
     ├── assets
     │   ├── ...
     ├── core
     │   ├── ...
     ├── pages
     │   ├── ...
     └── shared
         └── ...
```

--

#### Why did we refactor the whole project structure?

We did this for the sake of flexibility, scalability and decoupling.
We do not support the old `standard` project setup anymore.

--

#### Root Folder

In the root folder you can find the following files:

``` bash
.
├── ./Gruntfile.js
├── ./README.md
├── ./package.json
├── ./setup.json
├── ./veams-cli.json
└── ./yarn.lock
```

Most of the files are pretty self-explaining.

An important file is the `veams-cli.json`.
This file is new in the upcoming version and contains all necessary options and overrides for:

- veams-cli
- task configuration
- server configuration

--

#### Output folder

``` bash
.
├── app
│   ├── css
│   │   ├── app.css
│   │   └── app.css.map
│   ├── fonts
│   ├── icons
│   ├── media
│   └── scripts
│       └── app.bundle.js
```

Instead of the `_dist` and `_output` folders we now have the `app` folder.

We killed `libs.js` and renamed the final outcome from `main` to `app`. That's it!

--

#### Config Folder

``` bash
├── configs
│   ├── _grunt
│   │   ├── ...
│   ├── environments
│   │   ├── environment.dev.js
│   │   ├── environment.local.js
│   │   ├── environment.production.js
│   │   └── environment.qa.js
│   ├── tasks
│   │   ├── ...
│   └── templates
│       └── ...
```

`helpers` is now renamed to `configs`. Furthermore we added `environments` support for your application.

--

#### Server Folder

```bash
 ├── server
 │   ├── api
 │   │   ├── example
 │   ├── configs
 │   ├── content
 │   │   ├── ...
 │   ├── models
 │   ├── modules
 │   ├── services
 │   │   └── ...
 │   └── utils
```

In previous versions we had a simple server file. But we decided to provide a full stack solution with the following features:
- API support
- file based CRUD (Create/Read/Update/Delete) system
- proxy support
- simple extending possible

--

#### Source Folder

``` bash
└── src
    ├── app.events.js
    ├── app.js
    ├── app.scss
    ├── app.tmp.scss
    ├── app.veams.js
    ├── app.store.js (redux)
    ├── app.routes.js (single-page-app)
    ├── assets
    ├── core
    ├── features
    ├── pages
    └── shared
```

The source folder is the major working directory. Let's take a deep dive into that ...

--

**`core`** folder

The `core` is responsible for the project specific setup. It contains layouts, components and states which define the base of the application.

--

**`features`** folder

The `features` folder contains all specific application features which are purely self-contained.
Think of a complex module which could also act as a simple standalone project.

This folder will be mainly used in a  `single-page-app` type.

--

**`pages`** folder

The `pages` folder contains all pages of the application - simple.

--

**`shared`** folder

The `shared` folder contains files, that you want to share all over the project. Think of
- helper scripts (js, scss)
- dumb components (for single page apps)
- re-usage in different pages/features

--

#### App files

Next to the folders there live some app files.
These files are your global foundation and entry points for your project.

Let's have a look ...

![alt See](assets/img/open-eyes.gif "See")

--

**`app.scss`** file

We renamed `styles.scss` to `app.scss`. The `app.tmp.scss` will be generated automatically.

That's it ;)!


--

**`app.js`** file

We renamed `main.js` to `app.js`. This is the file where your modules get initialized.

--

**`app.events.js`** file

We renamed `events.js` to `app.events.js`. In this file you can save all global events.

--

**`app.veams.js`** file

We renamed `app.js` to `app.veams.js`. In this file you configure Veams and expose it to the other modules.

--

**`app.store.js`** file

When you choose `redux` as store handler you will get this file additionally.

It configures the whole store for you and exposes the store as a singleton.

--

**`app.routes.js`** file

When your project type is `single-page-app` you will get this file additionally.

--

#### Wtf - so much input

![alt Input](assets/img/input.gif "Input")

--

#### Exercise 01: Scaffold a new project

1. Goto folder /exercises/01-veams-cli-setup`
1. Scaffold a new project and select jQuery as JS lib and Bourbon Neat as SCSS framework (use defaults for all other prompts)
1. As soon as scaffolding process has finished start the project

---

## Veams-Cli - Components and Utilities

--

### Install process

- All Veams components and utilities are published on NPM: https://www.npmjs.com/org/veams
- Example page hosting all currently available components/utilities: http://examples.veams.org/

--

You can install existing Veams components and utilities like this:

```bash
veams install veams-component slider
```

```bash
veams install veams-utility grid
```

For details on available commands and short forms check Veams help in the terminal:

```bash
veams -h
```

--

#### Exercise 02: Installing Veams components

1. Goto folder `/exercises/02-veams-cli-components`
1. Install the following components `c-video`, `c-picture` and `c-figure`
1. Take a look at the components documentation pages linked on `http://localhost:3000/index.html`
1. Take also a look at the components overview page at `http://localhost:3000/components.html`
1. Take a look at the new component folders generated in `src/shared/components`

---

## Veams-Cli - Blueprints

One of the main features in our new `veams-cli` is the scaffolding part of blueprints.

Here we re-wrote the generator from scratch to provide a solid and really flexible base.

--

### Main features in a nutshell

- prompts can be easily extended by the developer
- developers can write their own templates
- installation of provided blueprint templates possible (currently in process)
- custom types? no problem!

Means, to scaffold blueprints is not limited to `Veams`.

You can use it in react, angular, vue, veams or even non javascript projects.

--

### Example





---

## VeamsComponent

`VeamsComponent` acts as base class for your custom components.

--

### Initial methods

--

#### constructor(obj)
- default options are defined here
- you have to call `super(obj, options)` to merge default with markup options

--

#### initialize()
- called on init
- useful for preparing your component

--

#### preRender()
- if needed templates can be prerendered here using `renderTemplate` (see section "Render templates")

--

#### bindEvents()
- bind events manually here using `registerEvent` (see section "Events / Manual binding")

--

#### render()
- called as long as option `render` is not set to `false` in options of module loader
- render your templates here or update the state of your component

--

### Lifecycle hooks

The VeamsComponent provides useful lifecycle hooks.

--

#### willMount()
- executed after initialize

--

#### didMount()
- executed after initial render

--

#### willUnmount()
- executed **before** unregistering events

--

#### didUnmount()
- executed **after** unregistering events

--

### Merging options
- default options defined in constructor will be merged with markup options by calling `super(obj, options)` in constructor
- markup options have higher priority and always overwrite default options properties of the same name

Example for overwriting default options with markup options:

``` html
<div
    data-js-module="slider"
    data-js-options='{
        "infinite": true,
        "pauseOnHover": false}'
>...</div>
```

--

### Subscribe
The `VeamsComponent` can subscribe to global events using the getter `subscribe`.
Global events can be triggered with `Veams.Vent.trigger('eventName')`.

Example for global event subscription:

``` js
get subscribe() {
	return {
		'{{Veams.EVENTS.resize}}': 'resizeFunction'
	};
}
```

--

### Events

Local events can be bound by using the getter `events`.

--

#### Example 1 (without event delegation)

``` js
get events() {
	return {
		'click': 'onClick'
	};
}
```

In this case the event listener is bound to `this.el` and executed as soon as the element itself or any of its children is clicked.

--

#### Example 2 (with event delegation)

``` js
get events() {
	return {
		'click {{this.options.specialBtn}}': 'onClick'
	};
}
```

In this case the event listener is also bound to `this.el` but only executed if element specified in option `specialBtn` is clicked.


--

### Manual event binding

Sometimes you need to bind events conditionally. Using the provided `registerEvent` method is a comfortable way.

Example of manually registering local event in automatically called `bindEvents`

``` js
bindEvents() {

	// register global event
	this.registerEvent('{{this.options.globalEvent}}', 'eventHandler', true);

	// register local event with event delegation
	this.registerEvent('{{Veams.EVENTS.keydown}} {{this.options.someSubComponent}}', 'onKeydown');
}
```

--


### Render templates

Rendering templates with Veams is pretty easy. You only have to specify the names of templates you want to use in the options of your component and then make a call to the `renderTemplate` function, passing the template name and the data as parameters.

``` js
render() {

	// render template with provided data
	let tmpl = this.renderTemplate('btn', data);

	// append output to current element
	this.$el.append(tmpl);
}
```

## Veams Framework

### SCSS

### JS

### Plugins

lorem ipsum



