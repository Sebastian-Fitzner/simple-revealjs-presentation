# React Basics I :: Introduction

Webpack, React, Redux, Routing, ExpressJS and Server Side Rendering from scratch.
 
--

## Sitemap

1. Setup
1. React
1. Router
1. Redux 

--

### Setup

1. Multiple ways to setup a project
1. Tools 
1. Hands-On

--

### React

1. Short Introduction to the Library/Framework
1. First Component & Setup
1. Component Structure
1. Lifecycle Hooks
1. Best Practices
1. Further Modules/Plugins

--

### Router
 
1. Basic Usage
2. Better Route Handling 

--

### Express 

1. Basics
1. Create API

--

### Redux

1. Short Introduction
1. Reducers, Actions, States, Selectors & Epics 
1. Setup
1. Best Practices

---

## Setup with Create-React-App

--

![alt Nooo](assets/img/react/nooo.gif "Nooo")

--

## Setup with Veams

--

![alt Nooot gonna happen](assets/img/react/not-gonna-happen.gif "Not gonna Happen")

--

## Do it from scratch?

-- 

![alt Yes](assets/img/react/yes.gif "yes")

--

### Let's start 

--

**Let's create a simple base to answer the following questions:**

1. How do I start?
1. How is the structure?
1. Which tools do I need to use?
1. Which packages do I need to install?
1. Do I need a server?

After that we improve our base step by step.

--

#### How do I start?

Create a new folder and init a new project by using `npm`.

```bash
npm init
```

Answer all questions and you have a new project. Great work!

--

#### How is the structure?

Because we start from scratch, we extend and refactor the folder and file structure from time to time. 

For now let's create the following: 

```bash 
.
├── app
│   └── scripts
└── src
    └── app
        └── core
            ├── containers
            └── layouts
```

--

#### Which tools do I need to use?

For React we need the following features: 

- JS Bundler
- ES6 Support 
- JSX Support

Later we will introduce:

- Decorators
- Class Properties

Let's give Babel and Webpack a try ...

_Do you know which tool is responsible for what?_

--

#### Which Packages do I need to install?

We need a few dev packages as well as the main libs. 

--

**So let us add the development packages:** 

```json
{
    "devDependencies": {
        "babel-core": "^6.26.0",
        "babel-loader": "^7.1.2",
        "babel-preset-env": "^1.6.1",
        "babel-preset-react": "^6.24.1",
        "babel-preset-stage-0": "^6.24.1",
        "npm-run-all": "^4.1.2",
        "webpack": "^3.10.0"
    }
}
```

-- 

**Next to that the libs**

```json
{
    "dependencies": {
        "react": "^16.2.0",
        "react-dom": "^16.2.0"
    }
}
```

--

#### Do I Need a Server?

--

![alt Sure](assets/img/react/sure.gif "sure")


--

For simplicity reason we use `http-server` which we are going to replace later with `express`: 

```bash
yarn add http-server --dev
```

---

## Webpack & Babel Configuration

--

_Why do we need Babel?_
 
Because we want to use next generation JavaScript, today ... and for writing React JSX syntax.
 
_Why do we need Webpack?_

Because a JavaScript bundler is necessary ... and this is used in almost all starter kits.

--

### Webpack Configuration File 

We should start to create a configuration file ...

-- 


```js 
const path = require('path');

module.exports = {
    // Entry point for webpack 
	entry: './src/app/app.js',
	// Output directory and filename
	output: {
		filename: 'app.bundle.js',
		path: path.resolve(__dirname, 'app/scripts')
	},
	// Tell webpack to run babel on every file it runs through
	module: {
		rules: [
			{
				test: /\.jsx?$/,
				loader: 'babel-loader',
				exclude: /node_modules/,
				options: { // Let's add babel presets and plugins 
					presets: [
						'react',
						'stage-0',
						['env', {
							targets: {
								browsers: ['last 2 version']
							}
						}]
					],
					plugins: [
						'transform-class-properties',
						'transform-decorators-legacy'
					]
				}
			}
		]
	}
};
```
--

### Testing

To test our configuration we should create a JS file in `src/app/`. 

Next to that we should add an HTML file and reference the file ... 

-- 

### NPM Scripts

To start the server and webpack we will need to execute a few bash commands. 

--

#### Start the server

To start a server is really simple: 

``` bash 
cd app && ./node_modules/.bin/http-server 
```

This can be saved in our `package.json`: 

``` json 
{
    "scripts": {
        "serve": "cd public && http-server"
    }
}
```

-- 

#### Start webpack to watch file changes

To work with wepack lets add the following: 

``` json 
{
    "scripts": {
        "dev:client": "webpack --config webpack.js --watch",
        ...
    }
}
```

--

#### Little improvements 

But I do not want to start all scripts independently. So therefore we have a simple solution, use `npm-run-all` as package. 

``` bash 
yarn add npm-run-all --dev
```

After that we can add a new script: 

``` json 
{
    "scripts": {
        ...,
		"start": "npm-run-all --parallel serve dev:*"
    }
}
```

-- 

![alt Let's get started](assets/img/react/start.gif "Let's get started")

--- 

## React

--

### Introduction

With React you can design simple views for each state in your application, and React will efficiently update and render just the right components when your data changes.

It is - of course - component-based!

--

#### It is a view library 

In its base it is just a view library. That makes it fairly easy to get something really fast up and running.

Just return your markup from a function or render method. 

-- 

#### You can handle states with it

It supports component enclosed state management and renders the view automatically when state is changed. 

-- 

#### You can pass properties

This feature is really powerful and a core functionality. Just pass props to components and work with them ... 

--

#### It extensively use HOC/HOF

React uses a lot Higher Order Components ... 

--

### Create a few components

Add the following structure:

```bash
├── src
│   └── app
│       ├── app.js
│       ├── core
│       │   ├── containers
│       │   │   └── core.js
│       │   └── layout
│       │       └── layout.js
│       └── pages
│           ├── article.js
│           └── home.js

```

---

### Routing

--

#### Link to pages

To work with references to pages we can use a component from `react-router-dom`. This component is called `Link`. 

Let's link our pages by using that component ...

--

#### Link Component 

Just import the component and add your links to the `layout` component: 

--

**Import**

``` js
import { Link } from 'react-router-dom';
```

--

**Usage**

``` html
<Link to="/">Home</Link>
<Link to="/article">Article</Link>
```

--

With that in place you can navigate through your application. 

---

### React Styling

For now we only have React in place. But we also need styling support. For that there are multiple ways possible:

1. CSS-in-JS
1. CSS Modules with(out) Webpack integration
1. SCSS with/out Webpack integration

--

#### CSS-in-JS

With that approach you can manage inline styles on React elements. It gives you powerful styling capabilities without CSS.

Libraries are:

- [Radium](https://formidable.com/open-source/radium/docs)
- [Aphrodite](https://github.com/khan/aphrodite)
- [react-with-styles](https://github.com/airbnb/react-with-styles)


More information: 
- http://jsramblings.com/2017/09/22/understand-the-react-styling-paradigms.html
- https://www.sitepoint.com/style-react-components-styled-components/
- https://www.sitepen.com/blog/2017/08/17/state-of-modern-component-styling/

--

**Documentation Example (react-with-styles)**

```js 
import React from 'react';
import { css, withStyles } from './withStyles';

@withStyles(({ color, unit }) => ({
  container: {
    color: color.primary,
    marginBottom: 2 * unit,
  },
}))
export default function MyComponent({ styles }) {
  return (
    <div {...css(styles.container)}>
      Try to be a rainbow in someone's cloud.
    </div>
  );
}
```

--

#### CSS Modules

Every CSS class is assigned a local-scoped identifier with a global unique name. CSS Modules enable a modular and reusable CSS!

--

**Documentation Example**

``` js
import React from 'react';
import styles from './table.css';

export default class Table extends React.Component {
    render () {
        return (
        <div className={styles.table}>
            <div className={styles.row}>
                <div className={styles.cell}>A0</div>
                <div className={styles.cell}>B0</div>
            </div>
        </div>
        );
    }
}
```

--

**Output**

``` html
<div class="table__table___32osj">
    <div class="table__row___2w27N">
        <div class="table__cell___1oVw5">A0</div>
        <div class="table__cell___1oVw5">B0</div>
    </div>
</div>
```

--

### SCSS

Create-react-app is not supporting SCSS. 

In general there is a discussion about using SCSS when you have scoped styles provided by other tools.

But I personally prefer that anyway because of:

- variables
- mixin support
- simple nesting
- and more ...

--

#### Multiple ways to work with SCSS

You can use Webpack to bundle it or just take a simple route by using one file where you collect all imports.

We go with the first one and set this up in a few minutes. 

--

#### Packages

Execute the following command to get all packages: 

``` bash
yarn add style-loader css-loader sass-loader node-sass --dev
```

--

To extract the compiled CSS into its own file you need to add our first plugin:

``` bash
yarn add extract-text-webpack-plugin --dev     
```

--

#### Webpack Configuration

Import the plugin: 
``` js
const ExtractTextPlugin = require('extract-text-webpack-plugin');
```

--

Add a new rule to webpack: 


``` js
{
    test: /\.(s*)css$/,
    use: ExtractTextPlugin.extract({
        fallback: 'style-loader',
        use: [ 'css-loader', 'sass-loader' ],
    })
}
```

--

And register the plugin:

``` js
plugins: [
    new ExtractTextPlugin({
        filename: 'css/app.bundle.css'
    })
]
```

--

To get it working the right way you need to update the `output` option like so:

``` js
output: {
    filename: 'scripts/app.bundle.js',
    path: path.resolve(__dirname, 'app')
}
```

--  

All together:

``` js
const path = require('path');
const ExtractTextPlugin = require('extract-text-webpack-plugin');


module.exports = {
	// Entry point for webpack
	entry: './src/app/app.js',
	// Output directory and filename
	output: {
		filename: 'scripts/app.bundle.js',
		path: path.resolve(__dirname, 'app')
	},
	// Tell webpack to run babel on every file it runs through
	module: {
		rules: [
			{
				test: /\.js$/,
				loader: 'babel-loader',
				exclude: /node_modules/,
				options: { // Let's add babel presets and plugins
					presets: [
						'react',
						'stage-0',
						[ 'env', {
							targets: {
								browsers: [ 'last 2 version' ]
							}
						} ]
					],
					plugins: [
						'transform-class-properties',
						'transform-decorators-legacy'
					]
				}
			},
			{
				test: /\.(s*)css$/,
				use: ExtractTextPlugin.extract({
					fallback: 'style-loader',
					use: [ 'css-loader', 'sass-loader' ],
				})
			}
		]
	},
	plugins: [
		new ExtractTextPlugin({
			filename: 'css/app.bundle.css'
		})
	]
};
```

--

### Start hacking around

With all that in place, we can add a general layout with a few styles ...

--

#### How to start?

**Create a scss file next to your component (`layout.scss`).**

--

**Add classes styles to the created file**
``` scss
/* ===================================================
Regions
=================================================== */
.r-header {
    background-color: aliceblue;

    .header__headline {
        font-size: 3rem;
        text-align: center;
    }
}

.r-main {
    margin: 1rem 0;
}

.r-footer {
    background-color: antiquewhite;
}
```
    
--

**Import file into component:** 
``` js
import './layout.scss';
```

--

**Use the classes in your component**
``` js
import React, {Fragment} from 'react';
import './layout.scss';

export default function Layout({children}) {
    return (
        <Fragment>
            <header className="r-header is-container">
                <h1 className="header__headline">My custom header</h1>
            </header>
            <main className="r-main is-container ">
                {children}
            </main>
            <footer className="r-footer is-container ">
                <h2>Footer</h2>
            </footer>
        </Fragment>
    )
}
```

--

__But wait, what is `<Fragment>`?__ 


When you work with `JSX` you have to return one main element which contains your markup: 

``` js
return (
    <div>
        My custom element. 
    </div>
)
```

This was not possible:

``` js
return (
    <div>first</div>
    <div>second</div>
    <div>third</div>
)
```

--

This problem leads to unnecessary markup and was bloating up your html.

But now you can use `Fragment` to get rid of it and use an empty element as main element.

---

## React Basics II :: Server Setup

--

1. ExpressJS Framework
1. Basics of ExpressJS
    - Packages
    - Server Setup
1. Development with Nodemon
    - Setup & Configuration
    - Improvements
1. Routing
1. Deliver HTML by ExpressJS
1. Assets

--

### ExpressJS Framework

Express is a fast, unopinionated, minimalist web framework for Node.js. 

So it means, you can run a web server with it ...

--

### Basics of ExpressJS - Packages 

To work with Express let us first install the dependencies: 

``` bash
yarn add express --save
```

Add a new file and folder: 

``` bash 
├── src
│   ├── app
│   └── server
│       └── index.js

```

After that we create a new npm script:
``` json
{
    scripts: {
        "dev:server": "node src/server/index.js"
    }
}
```

--

### Basics :: Setup

Now let us use Express and see if it is running. Therefore we need to add a few lines to `src/server/index.js`.

--

``` js
const express = require('express');
const app = express();

app.listen(3000, () => console.log('React server app listening on port 3000!'));
```

--

If you open up the browser, you should see `Cannot GET /`. Great, you have now a running server in place. 

--

**But what if you change the code?**

Nothing has changed in the browser, because NodeJS does not watch files and restarts itself. 

This is where Nodemon comes into ...

--

### Nodemon

is a monitor for any changes in your node.js application and automatically restart the server - perfect for development!

You now what is coming, right?!

--

#### A new package

![alt a new package](https://media.giphy.com/media/HhocXRaJRi7QI/giphy.gif "A new package")

``` bash
yarn add nodemon --dev
```

--

#### Do we need a configuration file? Of course ...

``` json
{
	"restartable": "rs",
	"ignore": [
		".git",
		"node_modules/**/node_modules"
	],
	"verbose": true,
	"execMap": {
		"js": "node --harmony"
	},
	"events": {
	},
	"watch": [
		"src/server/"
	],
	"ext": "js json"
}

```
--

#### NPM Script

What's left is the modification of the `dev:server` script: 

``` json
{
    scripts: {
        "dev:server": "nodemon src/server/index.js --config nodemon.config.json"
    }
}
```

Furthermore we can delete the the `serve` script. 

--

**Now when you change files, the server gets restarted.**

--

#### Improvements

So Nodemon is easy to setup and for development purpose a nice tool. Later we will improve the startup of our node application by using `PM2`. 

With `PM2` you can 
 - monitor multiple applications
 - enable a cluster mode to load balance your application
 - restart your applications 
 - startup scripts

--

### Routing

For now we only have an error message shown up. Let's dive into our code and add our major route. 

--

Adding a route is really easy: 

``` js
/**
 * Routes
 */
app.get(['*'], (request, response) => response.send('Hello world'));

```

You can see that we can use wildcards (`*`) in here, which means I want to show on every route `Hello world`.

--

### Deliver HTML by ExpressJS

_But we have already an HTML file, can we use it?_

Sure, we just read the file with NodeJS and send the content back as response.

-- 

#### Read files from the filesystem

Let's move the index.html to `src/server`. Then start to read out the file and return the content: 

``` js
const fs = require('fs'); // Require a core module to work with the filesystem
const html = fs.readFileSync(__dirname + '/index.html', 'utf-8'); // Read the file synchronously and use `__dirname` to work with the folder, where the index.js is located.

/**
 * Routes
 */
app.get(['*'], (req, res) => res.send(html));
```

--

### Assets

_But JavaScript and Styles are not working anymore._

You are right, because `Express` needs to know where our assets are located.  

--

#### Add static assets 

By adding the following script everything should work like expected: 

``` js
/**
 * Static Asset Location
 */
app.use(express.static('./app'));

```

--

**Here we go, a running NodeJS server is in place and fully functional.**

![alt Great work](https://media.giphy.com/media/xT9DPxPZnDcBMX6tAk/giphy.gif)

---

## React Basics III

### API, Services & a few components

---

## Demo Time

**Come on, let's create a simplified Netflix application on our own.**

--

Let's take a look at what we want to achieve in this meeting. 
Checkout `feature/moviefy@0.0.1-alpha`, install all packages and start the project. 

You should see a simple home page displaying the **Top Rated Movies**. 


--

### Requirements

To achieve that, we need to do the following...

--

#### NodeJS (Server Side)

- Create an API endpoint for movies
    - use `router` to separate the logic
- Create a proxy to work with https://www.themoviedb.org/
    - create an account to get an API key 
        - User: ApertoDev, PW: aperto123
        - API-key V3: 2b81dd87d05206bc0da697f603ebce88
- Add cache for API endpoint

--

#### React :: Service (Client Side)

- Add our first http service
- Update home page to display summary with `teaser` component

--

#### Configuration

- Add Sass globbing
- Add copy task

-- 

#### React :: Make it look nice (Client Side)

- Add a `grid`
- Add `logo`, `navigation`, `navigation-toggle`, `section`
- Add height calculation for navigation overlay

-- 

## Let's fasten our seat belts!

![alt Fasten Seat Belts](https://media.giphy.com/media/3oEjHYU0qqJL3KosHC/giphy.gif)

---

## API

Let's create our first API endpoint. For that we want to use real data from another API. 

That means we will need to use NodeJS as proxy and forward the request ... 

--

### Create the endpoint in our server

This is a fairly simple task. We use `request` to get the data from an external API and pipe it through ...

--

**Register `api` endpoints by creating necessary files and adding a new route.**

--


``` js
const apiRoutes = require('./api');

/**
 * Api Routes
 */
app.use('/api', apiRoutes);
```

--

**Use router to attach new routes to our express server, for example `/api/test`.**

--

``` js
const { Router } = require('express');
const router = new Router();

router.get('/test', (req, res) => {
	res.send({
		test: "tst"
	})
});

module.exports = router;
```

--

**Add a simple proxy handler by using `request`.** 

_Install all necessary dependencies by using `yarn add request --save`._

--

``` js
const { Router } = require('express');
const request = require('request');
const router = new Router();

/**
 * Add API
 */
router.get('/discover/movies', (req, res) => {
	return request
		.get('https://veams.org')
		.on('error', () => res.sendStatus(503))
		.pipe(res)
});

module.exports = router;
```

--

### Discover the API

To understand what we need to do, there is a [documentation](https://www.themoviedb.org/documentation/api), of course.

Even better: https://developers.themoviedb.org/3/getting-started/introduction

Let's take a look at it and how you can work with it. 

--

### URL Pattern

The URL Pattern is simple as well: 

``` bash
https://api.themoviedb.org/3/movie/top_rated?page=1&language=en-US&api_key=2b81dd87d05206bc0da697f603ebce88
```

Let's integrate that on the server side. 

--

``` js
/**
 * Add API
 */
router.get('/movies/top-rated', (req, res) => {
	console.log('Movies API :: Execute request to top rated movies!');

	const options = {
		url: 'https://api.themoviedb.org/3/movie/top_rated',
		qs: {
			page: '1',
			language: 'en-US',
			api_key: '2b81dd87d05206bc0da697f603ebce88'
		},
		body: '{}'
	};
	return request
		.get(options)
		.on('error', () => res.sendStatus(503))
		.pipe(res)
});
```

--

### Add Cache

Last but not least, we want to add the cache middleware. 

For that we install `apicache` by executing:

``` bash 
yarn add apicache --save
```

--

*Side Note*

Middlewares can be easily added and written in Express by executing `res.next()` and passing that function in our route. 

--

``` js
const apicache = require('apicache');
const cache = apicache.middleware;

app.use('/api', cache('3 Minutes'), apiRoutes);
```

---

## React (Client Side)

Now that we have our server well prepared, let's start to work on the client side. 

--

### Http Service

To work with our new API endpoint we need to work with async http requests. 

There are multiple ways to do that (`fetch`, `axios`, `veams-services`). 

--

**Let's add the last one by executing `yarn add veams-services --save`.**

--

**Create a new service which can be shared among the project.**

_Wanna use `await` and `async`? Add a polyfill or modify the settings like so:_

``` js
[ 'env', {
    targets: {
        browsers: [ 'last 2 Chrome versions' ]
    }
} ]
```

--

``` js
import VeamsHttp from 'veams-services/lib/http';
const httpService = new VeamsHttp({
	type: 'json'
});


class MovieService {
	url = 'http://localhost:3000/api/movies/top-rated';
	http = httpService;

	/**
	 * Get Top Rated Movies
	 */
	async getTopRated() {
		try {
			return await this.http.get(this.url);
		} catch(err) {
			console.error('MovieService :: Error in getting top rated movies\n', err);
		}
	}
}

const movieService = new MovieService();

export default movieService;
```


--

**Update the home page and add the service.**

--

``` js
import React, { Component, Fragment } from 'react';
import { movieService } from '../shared';

export default class Home extends Component {
	state = {
		topRated: []
	};

	async componentDidMount() {
		try {
			const data = await movieService.getTopRated();

			this.setState(() => ({
				topRated: data.results
			}))
		} catch (err) {
			console.log('Error in getting files for Home page!');
		}
	}

	render() {
		return (
			<Fragment>
				<div className="teasers">
				</div>
			</Fragment>
		)
	}
}
```

--

**Create a teaser list to display the summary.**

--

``` js
import React, { Component, Fragment } from 'react';
import { movieService } from '../shared';

export default class Home extends Component {
	...

	render() {
		return (
			<Fragment>
				<div className="teasers">
					{teasers(this.state.topRated)}
				</div>
			</Fragment>
		)
	}
}

/**
 * Teasers Partial
 */
function teasers(teasers) {
	return teasers.map(teaser => (
		<div className="teaser" key={teaser.id}>
			<h3>{teaser.title}</h3>
			<img src={`https://image.tmdb.org/t/p/w500/${teaser.poster_path}`} alt={teaser.title}/>
			<p>
				{teaser.overview}
			</p>
		</div>
	))
}
```

---

## Configure Project

To simplify the work with general stylesheets by adding globbing support we need to update webpack. 

Furthermore we want to copy asset files automatically.

--

### Sass Globbing

For that we install [`node-sass-magic-importer`](https://github.com/maoberlehner/node-sass-magic-importer). 
This is a module which I discovered two weeks ago and it looks very promising. 

You can import 
- files by using globbing patterns `shared/**/*.scss`.
- classes, functions, mixins or anything else like in JavaScript

The problem is, that it does not create any watchers for directories.

--

``` js 
const magicImporter = require('node-sass-magic-importer');

...
{
    test: /\.(s*)css$/,
    use: ExtractTextPlugin.extract({
        fallback: 'style-loader',
        use: [
            {
                loader: 'css-loader'
            }, {
                loader: 'sass-loader',
                options: {
                    importer: magicImporter(),
                }
            }
        ],
    })
}
```

--

### Copy Task for Assets

To copy files between directories we use another plugin for Webpack. 

``` bash 
yarn add webpack-copy-plugin
```

--

After that it is enough to add that to the plugins array. 

--

``` js
const CopyWebpackPlugin = require('copy-webpack-plugin');

...
plugins: [
    // Copy asset files from src/app
    new CopyWebpackPlugin([ {
        from: `src/app/assets`,
        ignore: [ '.gitkeep' ]
    } ])
]

```
--

### Now we are prepared for the rest ...
 
![alt Great work](https://media.giphy.com/media/3ohhwJ3wZCQwiPzmbC/giphy.gif)

---

## React :: Clean Up
 
### Add new Components

--

**Add a `grid`**

You can use any React component or framework you want to, for example: 

- React Grid System
- Bootstrap
- Foundation
- veams-utility-grid or Bourbon Neat

Let's add a SCSS based grid, because I like the simplicity of CSS and do not need a component for that: 

``` bash
yarn add veams-utility bourbon bourbon-neat@2.1.0 --save
```

--

Import all libraries to a global `app.scss` file. Do not forget to import that file into `app.js`.

--

``` scss
@import '../../node_modules/bourbon/core/bourbon';
@import '../../node_modules/bourbon-neat/core/neat';
@import '../../node_modules/veams-utility-grid/styles/grid';
```

--

**Add `logo`, `navigation`, `navigation-toggle`, `section`**

--

**Add height calculation for navigation overlay**

