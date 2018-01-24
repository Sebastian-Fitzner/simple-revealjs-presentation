# Veams Workshop

---

## Presentation online

This presentation can be found at https://showroom.aperto.de/projects/p/Presentations/veams-workshop-2017

You need credentials to get access:

1. Login to https://showroom.aperto.de/ with your default Aperto credentials
1. Search for "Presentations" and use corresponding KundenId and KundenPW

---

## Sitemap

1. What is the workshop (not) about?
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

### Veams-Cli

To scaffold a project or blueprints like components you can use `veams-cli`.

See https://www.npmjs.com/package/veams-cli for an overview.

--

### Veams

To work with JavaScript and SCSS you have to use `Veams`.

The current version is v5.xx and you can find the documentation and package at https://github.com/Veams/veams.

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

Install veams-cli globally by executing `npm i -g veams-cli@next`.

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
 ├── environments
 │   ├── ...
 └── src
     ├── app
     │   ├── assets
     │   │   ├── ...
     │   ├── core
     │   │   ├── ...
     │   ├── pages
     │   │   ├── ...
     │   └── shared
     │       └── ...
     └── server
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

#### veams-cli.json

The file looks like that:

``` json
 {
     "projectType": "static-page-app", // Project type definition
     "blueprints": { // Define custom blueprints
         "filePrefix": false
     },
     "config": {
         "src": "configs/_grunt/*.js" // Config task files
     },
     "importFiles": { // Files where references are created
         "style": "src/app.scss",
         "script": "src/app.js"
     },
     "insertpoints": [ // Files & Folders where to search for INSERTPOINTS
         "src/app.js",
         "src/shared/layouts",
         "src/pages",
         "src/features/containers",
         "src/app.events.js"
     ],
     "paths": { // Path configuration
         "config": "configs",
         "server": "server",
         "src": "src",
         "app": "app",
         "component": "src/shared/components",
         "utility": "src/shared/utilities"
     },
     "ports": { // Ports
         "app": 3000,
         "server": 2999
     },
     "startPath": "index.html" // Redirect path in server
 }
```
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
│   ├── img
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
│   ├── tasks
```

`helpers` is now renamed to `configs`. 
We decided to go away a bit from task runner specific plugins and created simple `npm` scripts.

--

### Environments Folder 
Furthermore we added `environments` support for your application.

```bash 
environments
├── environment.dev.js
├── environment.local.js
├── environment.production.js
└── environment.qa.js

```
--

### src Folder

The `src` folder contains the server and application code. 

--

### Server Folder

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

#### App Folder

``` bash
└── app
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

The app folder is the major working directory. Let's take a deep dive into that ...

--

**`core`** folder

The `core` is responsible for the project specific setup. 
It contains layouts, components and states which define the base of the application.

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

If not done yet - please checkout https://github.com/aperto-frontend/veams-workshop-2017.git first

1. Goto folder `/exercises/01-veams-cli-setup`
1. Scaffold a new project and select **jQuery** as JS lib and **Bourbon Neat** as SCSS framework (use defaults for all other prompts)
1. As soon as scaffolding process has finished start the project

---

## Veams-Cli - Components and Utilities

--

### Install process

- All Veams components and utilities are published on **npm**: https://www.npmjs.com/org/veams
- **Example page** hosting all currently available components/utilities: http://examples.veams.org/

--

You can install existing Veams components and utilities like this:

_Components_
``` bash
veams install veams-component slider
```

``` bash
veams -i vc slider
```

 _Utilities_
``` bash
veams install veams-utility grid
```

``` bash
veams -i vu grid
```
For details on available commands and short forms check Veams help in the terminal:

``` bash
veams -h
```

--

#### Exercise 02: Installing Veams components

1. Stay in your folder or go to folder `/exercises/02-veams-cli-components`
1. Install all packages using `yarn install` or `npm install`
1. Install the following Veams components `c-video`, `c-picture` and `c-figure`
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
- custom types? No problem!

--

Means, to scaffold blueprints is not limited to `Veams`.

You can use it in react, angular, vue, veams or even non javascript projects.

--

![alt What?!](assets/img/wait-what.gif "What?!")

--

### Example

Pre-Condition is a SPA with Redux in place.

Let's say you have a module called articles and you want to add a store slice to that module, then you can use Veams-Cli to do that automatically for you by using a blueprint.

How? Let's make our life easy by adding a provided blueprint template called `veams-bp-redux`.

--

#### Install a Blueprint

`yarn add veams-redux-blueprint --dev`

--

#### Add the Blueprint to Veams

You just need to add your new blueprint to `veams-cli.json`:

``` json
{
	...,
	"blueprints": {
		"filePrefix": false,
		"store": {
			"skipImports": true,
			"prompts": "node_modules/veams-redux-blueprint/prompts",
			"templates": "node_modules/veams-redux-blueprint/templates"
		}
	}, ...
}
```

- When you add `skipImports` Veams-Cli automatically skip the process to import a reference in `app.js`.
- `prompts` are customized questions for this blueprint.
- `templates` are store specific templates written in `EJS`.

--

#### Scaffold it!

``` bash
veams add store features/article
```

--

#### Output

Here it comes. A lot of files are auto generated in a few seconds:

``` bash
├── features
│   └── article
│       ├── services
│       │   └── article.service.js
│       └── store
│           ├── article.actions.js
│           ├── article.epics.js
│           ├── article.reducer.js
│           ├── article.selectors.js
│           └── article.state.js
```

--

### Boom

![alt Boom](assets/img/boom.gif "Boom")

--

### Available Blueprints 

We have a few blueprints already published. These can be found on Github, in our npm organisation or via search:

https://www.npmjs.com/search?q=veams-bp

--

### But how do you add a custom type?

You should know, that every type is a custom type now - even the standard component. There is no difference anymore.

So let's make the picture clear with another example and by doing it from scratch.

--

### Define a Type

Because in this presentation are always gifs, I really need a giphy blueprint. 
This blueprint should help me out in generating a new giphy component.

That's why we will create a type which we call `giphy`. Add that to the key `blueprints` in your `veams-cli.json`:

```json
{
    ...,
	"blueprints": {
		"store": {...},
		"giphy": {
			"skipImports": true,
			"prompts": "configs/blueprints/giphy/prompts",
			"templates": "configs/blueprints/giphy/templates"
		}
 	},
 	...
}
```
--

You have probably seen, that we saved a path to the prompts and templates files. So we need to create these.

--

#### prompts.js file

The `prompts.js` file is just a function which returns an array of prompts in there.

So let us create 2 questions:

1. Which gif do you like to choose?
1. Which background color do you want to use?

--


``` js
module.exports = (context) => {
	return [
		{
			type: 'list',
			name: 'giphyName',
			message: 'Which gif do you want to choose?',
			choices: [
				{
					name: 'Happy',
					value: 'happy'
				},
				{
					name: 'Sad',
					value: 'sad'
				},
				{
					name: 'Angry',
					value: 'angry'
				}
			]
		},
		{
			type: 'input',
			name: 'giphyColor',
			message: 'Which background color do you want to use?',
			default: 'black'
		}
	];
};
```

--

#### Template files

The template files will be automatically read by Veams-Cli. You can add as many as you want in the `templates` folder.

You can create a structure like you want in that folder. Veams-Cli keeps that structure for you.

Every file in there has to be named with `bp` when you want to generate the name based on your input.

--

#### Structure of a blueprint

``` bash
.
└── giphy
    ├── prompts.js
    └── templates
        ├── bp.hbs.ejs
        └── styles
            └── bp.scss.ejs

```

--

#### Variables

To work with templates you get standard variables you can use. These are:

--

- `props` = all properties
- `skipFiles` = skip file option
- `path` = path to file
- `name` = blueprint name
- `customTypeName` = type of blueprint
- `customTypePrefix` = prefix of blueprint
- `filename` = filename of blueprint
- `bpName` = camel cased name
- `bpNameUppercase` = uppercased name
- `bpJsName` = pascal cased name

--

Next to these standard variables you will get your custom values as well. They are located under `props`.

--

##### Template

``` hbs
<%
var url = '';

if (props.giphyName === 'sad') {
    url = 'https://media.giphy.com/media/d2lcHJTG5Tscg/giphy.gif'
} else if (props.giphyName === 'happy') {
    url = 'https://media.giphy.com/media/UkhHIZ37IDRGo/giphy.gif'
} else {
    url = 'https://media.giphy.com/media/26tnnpcYVRNJGlHy0/giphy.gif'
}
%>
<div
    class="giphy--<%= filename %> is-<%= props.giphyName %>"
    style="background-color: <%= props.giphyColor %>">
	<img
	    src="<%= url %>"
	    alt="<%= props.giphyName %>">
</div>
```

--

#### Terminal

By executing `veams add giphy yellow-gif` we will get the following prompts:

--

``` bash
# sebastian.fitzner @ C02SGJPFG8WP in ~/projects/exercises/v9-static [0:08:44]
$ veams add giphy shared/components/yellow-gif

==================================================
Starting to scaffold a new giphy  ...
==================================================


Create a new blueprint based on Veams or your own templates.

? Which gif do you want to choose? (Use arrow keys)
  Happy
❯ Sad
  Angry

```

--

``` bash
# sebastian.fitzner @ C02SGJPFG8WP in ~/projects/exercises/v9-static [0:08:44]
$ veams add giphy shared/components/yellow-gif

==================================================
Starting to scaffold a new giphy  ...
==================================================


Create a new blueprint based on Veams or your own templates.

? Which gif do you want to choose? Sad
? Which background color do you want to use? (black)
```

--

```bash
# sebastian.fitzner @ C02SGJPFG8WP in ~/projects/exercises/v9-static [0:08:44]
$ veams add giphy shared/components/yellow-gif

==================================================
Starting to scaffold a new giphy  ...
==================================================


Create a new blueprint based on Veams or your own templates.

? Which gif do you want to choose? Sad
? Which background color do you want to use? black
? Which files do you want to skip? (Press <space> to select, <a> to toggle all, <i> to inverse selection)
❯◯ /gif.hbs file

```

--

#### Output

``` hbs
<div class="giphy--gif is-sad" style="background-color: black">
	<img src="https://media.giphy.com/media/d2lcHJTG5Tscg/giphy.gif" alt="sad">
</div>
```

--

## Exercise 1

1. Install the `veams-bp-redux` and add the paths to `veams-cli.json`. Call the key `store`.
2. Scaffold one store slice to `features/articles`
    - by executing `veams add store features/articles`
    - _INFO: the folder does not exists, so Veams-Cli will create that for you_

--

## Exercise 2

 1. Create your own blueprint. You can use the `giphy` example if you want to. Another good one would be a page blueprint. 

---

## Veams Framework

The purpose of Veams is to individually build up a project based framework in a simple, fast, scalable and understandable way.

--

Long time ago we had `Veams-SCSS` and `Veams-JS`. But we decided to put these together as Framework and add more functionality to it.

--

The outcome is now a standalone package called `veams`.

--

### SCSS

SCSS is located at `veams/src/scss`. From there you can import Animations, Resets, Defaults and more.

A good documentation can be found here: https://www.veams.org/sass/docs/_output/index.html

--

### JavaScript Framework


The core of Veams is nothing more than a simple JavaScript object (Veams). 
In general Veams comes with some empty and predefined objects and a basic API.

https://github.com/Veams/veams#veams-core-api

--

The most important part of Veams is the following functionality:

``` js
Veams.use()
```

With that function you can initialize your own plugins to extend `Veams`.

--

### Plugins

Veams comes with a handy plugin system, allowing you to easily add, load and configure plugins to fit your needs.
On the next slides we give you a short overview of the main plugins shipped with Veams.

--

#### veams-plugin-dom

The VeamsDOM plugin is simple plugin for which you need to pass a DOM handler like jQuery. For some other plugins VeamsDOM is a requirement.

Github: https://github.com/Veams/veams-plugin-dom

--

##### Usage

``` javascript
import $ from 'jquery';
import Veams from 'veams';
import VeamsDOM from 'veams/lib/plugins/dom';

// Intialize core of Veams
Veams.onInitialize(() => {
    // Add plugins to the Veams system
    Veams.use(VeamsDOM, {
        DOM: $
    });
});


// Usage in any other file
Veams.$('body').addClass('dom-handler-loaded');
```
--

#### veams-plugin-logger

The VeamsLogger plugin disables `console` logs by default. You can provide parameters (`?devmode`) in the URL to show the logs in your console.
Once enabled by parameter the devmode is persistent for the current session.

If devmode is enabled the additional parameter `&logger` adds a sticky console output element on the bottom of the page.
This could be useful for quick debugging on mobile devices.

Github: https://github.com/Veams/veams-plugin-logger

--

``` js
import $ from 'jquery';
import Veams from 'veams';
import VeamsDOM from 'veams/lib/plugins/dom';

// Intialize core of Veams
Veams.onInitialize(() => {
    // Add plugins to the Veams system
    Veams.use(VeamsLogger);
});
```

--

#### veams-plugin-media-query-handler

The VeamsMediaQueryHandler plugin provides to you a possibility to get the current media query name from your css.
Media query name and the corresponding breakpoints are retrieved from `_get-media.scss`.

Github: https://github.com/Veams/veams-plugin-media-query-handler

--

#### veams-plugin-mixins

The VeamsMixins plugin is something where you can save global mixins. Mixins are object with functions in it which can be used to extend methods in other classes/modules.

The `imageLoader` mixin for example can be applied to any class (component) which needs to update its view after all images had been loaded.

Github: https://github.com/Veams/veams-plugin-mixins

--

#### veams-plugin-modules

The VeamsModules plugin provides a whole system to initialize, render, save and destroy your modules.
It uses mutation observer to observe added and removed nodes and handles your components, as long as the component has the same API like the `VeamsComponent`.

This module is really helpful in a lot of things like conditional initialization, automatic initialization when the DOM gets updated and so on.

Github: https://github.com/Veams/veams-plugin-modules

--

##### Initializing

There are two ways to register modules with the plugin.

**Array Handling**

``` js
Veams.modules.register([
	{
		namespace: 'accordion',
		module: Accordion
	},...
]);
```

**Simple Handling**

``` js
Veams.modules.add({namespace: 'accordion', module: Accordion});
```

--

##### Conditional Initialization

You can easily initialize modules on conditions:

``` js

Veams.modules.register([
	{
		namespace: 'accordion',
		module: Accordion,
		conditions: () => Veams.detections.width > 700,
		conditionsListenOn: [
		    Veams.EVENTS.resize
		]
	},...
]);
```

--

##### Skip `render()`

You want skip render? Here you go:

``` js

Veams.modules.register([
	{
		namespace: 'accordion',
		module: Accordion,
		render: false
	},...
]);
```

--

#### veams-plugin-store

The store is relatively new, but it provides a simplified version of `redux`.

Github: https://github.com/Veams/veams-plugin-store

For more details you can also take a look at this presentation:

https://showroom.aperto.de/projects/p/Presentations/store-observable-pattern/

- User: 1860920541
- Password: R8NBzzJkZIki4RN

--

#### veams-plugin-templater

This plugin adds the possibility to render your `handlebars` templates in an easy way. You can register the engine, templates, partials and helpers and use them directly in your other classes.

Github: https://github.com/Veams/veams-plugin-templater

--

#### veams-plugin-vent

The VeamsVent plugin is a global publish and subscribe object. You can use this plugin to communicate between modules independently.

Github: https://github.com/Veams/veams-plugin-vent

--

### VeamsComponent

`VeamsComponent` acts as base class for your custom components.

--

#### Initial methods

--

##### constructor(obj)
- default options are defined here
- you have to call `super(obj, options)` to merge default with markup options

--

##### initialize()
- called on init
- useful for preparing your component

--

##### preRender()
- if needed templates can be prerendered here using `renderTemplate` (see section "Render templates")

--

##### bindEvents()
- bind events manually here using `registerEvent` (see section "Events / Manual binding")

--

##### render()
- called as long as option `render` is not set to `false` in options of module loader
- render your templates here or update the state of your component

--

#### Lifecycle hooks

The VeamsComponent provides useful lifecycle hooks.

--

##### willMount()
- executed after initialize

--

##### didMount()
- executed after initial render

--

##### willUnmount()
- executed **before** unregistering events

--

##### didUnmount()
- executed **after** unregistering events

--

#### Merging options
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

#### Subscribe
The `VeamsComponent` can subscribe to global events using the getter `subscribe`.
Global events can be triggered with `Veams.Vent.trigger('eventName')`.

Example for global event subscription:

``` js
get subscribe() {
	return {
		'{{Veams.EVENTS.resize}}': 'onResize'
	};
}
```

--

#### Events

Local events can be bound by using the getter `events`.

--

##### Example 1 (without event delegation)

``` js
get events() {
	return {
		'click': 'onClick'
	};
}
```

In this case the event listener is bound to `this.el` and executed as soon as the element itself or any of its children is clicked.

--

##### Example 2 (with event delegation)

``` js
get events() {
	return {
		'click {{this.options.specialBtn}}': 'onClick'
	};
}
```

In this case the event listener is also bound to `this.el` but only executed when the element is clicked which is predefined as `specialBtn` in options.

--

#### Manual event binding

Sometimes you need to bind events conditionally. Using the provided `registerEvent` method is a comfortable way.

Example of manually registering local event in automatically called `bindEvents`

``` js
bindEvents() {
	...

	if (condition) {
	
		// register global event
		this.registerEvent('{{this.options.globalEvent}}', 'eventHandler', true);
	
		// register local event with event delegation
		this.registerEvent('{{Veams.EVENTS.keydown}} {{this.options.someSubComponent}}', 'onKeydown');
	}
	
	...
}
```

--

#### Render templates

Rendering templates with Veams is pretty easy. You only have to specify the names of templates you want to use in the options of your component and then make a call to the `renderTemplate` function, passing the template name and the data as parameters.

``` js
render() {

	// render template with provided data
	let tmpl = this.renderTemplate('btn', this.data);

	// append output to current element
	this.$el.append(tmpl);
}
```

--

### Exercise: Scaffold a new component

Let's take a look inside of a Javascript component by scaffolding a new component with

``` bash
veams add component whatever
```

Now the component can be found in `src/shared/components/whatever`.

Play around with the lifecycle hooks and `conditions`.

--

### What has changed?

With the updated component blueprint we got now the following structure in `whatever`:

``` bash
.
├── INSERTPOINTS.md
├── README.md
├── data
│   └── whatever.json
├── scripts
│   └── whatever.js
├── styles
│   └── whatever.scss
├── templates
│   └── whatever.hbs
└── whatever.settings.json

```

--

1. No file prefixes anymore. But we think about an option if necessary.
    - This does not mean, that we do not use the class methodology of Veams.
1. YAML data is now saved in `whatever.settings.json`.
    - That makes it easy for us to share the partial in frontend and backend rendering.
1. New folder structure
    - Perhaps we will add here an option to flatten the directory.

--

Furthermore we support JavaScript features like:

- Class Properties
- Decorators Support

---

### Roadmap

1. Clean Up/ Stable Release | 12/2017
    - Context Property (Veams)
    - Webpack Support (Veams-Cli)
1. Veams Decorators (new package) | 1/2018
1. TypeScript Support (Veams-Cli, Veams) | 3/2018
1. Blueprint Templates (new packages) | ongoing
    - React Component BP
    - Veams Page BP
    - NGRX Store BP
1. Documentation | (12/2222)

---

## Mock API

With the new setup in place you have a mock api available where you can perform CRUD operations against it.

Everything is saved at the file system. We created that for `Globeswift` & `Connected Van` ...

--

###  Structure

The inner server folder looks like that:

``` bash
.
├── api // Custom API endpoints which are available
│   ├── example // Available at http://localhost:3000/api/examples
│   │   ├── controller.js
│   │   ├── index.js
│   │   └── model.js
│   └── index.js
├── configs // Custom server config
│   └── config.js
├── content // Content Routes & Proxy Example
│   ├── home.js
│   ├── index.js
│   └── server-hosts.js
├── index.js
├── mocks // Mock JSON files
│   └── example // Connected to API endpoint `example`
│       ├── 01.json
│       └── 02.json
├── models
│   └── api-model.js
├── modules // Modules to render routes and configure express
│   ├── express.js
│   └── mangony.js
├── services
│   └── response
│       └── index.js
└── utils
    └── helpers.js
```