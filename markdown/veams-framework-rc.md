# Veams as Framework

--

## Sitemap

1. What does "Veams as Framework" mean?
2. What are the enhancements?
3. First look
4. Used in ...

---

## What does "Veams as Framework" mean?

Only that we kicked out the starter kits (Veams-JS, Veams-Sass) and replaced these with a solid framework.
Just import the libs and you can start.

---

### What are the enhancements?

- No configuration at all (only if you want to)
- Easy to install (`npm i veams --save`)
- Pluggable system (everything is a plugin)
- Advanced module handling (mutation observer, unbinding of events, cache system, conditional loading with event support)
- Base classes, VeamsComponent class, VeamsHttp service class

---

## First look

Let's take a first look into it:

--
__app.js__

```js
import Veams from 'veams';
```
__styles.scss__
``` scss
// Reset (veams-reset or veams-normalize)
@import "../../node_modules/veams/src/scss/veams-reset";
@import "../../node_modules/veams/src/scss/veams";
```

With that in place you have the standard core already enabled. That means:

- Veams will be saved as namespace to the global window object
- Standard helpers are already in place
- The plugin system is enabled

--

**But that is not so much, right?! Let's add plugins to the system and see how we can get the most out of it.**

--

Let's start with the standard plugins which we already used in the starter kit (Veams-JS):

- VeamsLogger _(disable logs and show them when adding `?devmode` parameter to your url)_
- VeamsDOM _(add a custom DOM handler like jQuery)_
- VeamsVent _(global publish/subscribe system)_
- VeamsModules _(handle initialising and destroying of modules)_
- VeamsMediaQueryHandler _(Get the breakpoint names out of CSS)_

--

On a code base it looks like that:

```js
// Global dependencies
import {default as $} from 'jquery';
import Veams from 'veams';
import VeamsLogger from 'veams/src/js/plugins/logger';
import VeamsDOM from 'veams/src/js/plugins/dom';
import VeamsVent from 'veams/lib/plugins/vent';
import VeamsModules from 'veams/lib/plugins/modules';
import VeamsMediaQueryHandler from 'veams/src/js/plugins/media-query-handler';

Veams.onInitialize(() => {
	/**
	 * Veams Plugins
	 */

	// Dom Plugin
	Veams.use(VeamsDOM, {
		DOM: $
	});

	// Vent Plugin
	Veams.use(VeamsVent);

	// Logger Plugin for devmode and logger
	Veams.use(VeamsLogger);

	// Module System Plugin
	Veams.use(VeamsModules, {
		useMutationObserver: true,
		internalCacheOnly: false
	});

	// Media Query Handler Plugin
	Veams.use(VeamsMediaQueryHandler);
});
export { Veams };

```

-- 

**With that in place we can do everything we need to work with our project. Let's extend the base helpers.**

--

**app.js**

```js
import detectSwipe from 'veams/src/js/utils/helpers/detect-swipe';

Veams.onInitialize(() => {
	Veams.addHelper('detectSwipe', detectSwipe);
});
```

--
**Now let's register some custom components ...**
--

**main.js**

```js
// Global dependencies
import {Veams} from './app';

console.log('Veams initialized in version:', Veams.base.version);

// Imports
import Slide from '../templating/partials/components/slide/js/slide';
import Tester from '../templating/partials/components/tester/js/tester';
// @INSERTPOINT :: @ref: js-self-contained-import, @keep: true //

// Initialize modules with Veams
Veams.modules.register([
	// Init Slide
	{
		namespace: 'slide',
		module: Slide
	},
	// Init Tester
	{
		namespace: 'tester',
		module: Tester
	}
	// @INSERTPOINT :: @ref: js-init-v5, @keep: true //
]);
```
Sounds familiar?! I hope so.
--

Now let's take a look at conditional loading - a new feature:

```js
Veams.modules.register([
	// Init Slide
	{
		namespace: 'slide',
		module: Slide,
		conditions: () => { 
		    return Veams.detections.width > 1024; 
		},
		 conditionsListenOn: [ 
		    Veams.EVENTS.resize, 'custom' 
		]
	}
]);
```

--

Furthermore Veams provides some classes which you can work with:
- Base Class
- VeamsComponent Class
- VeamsHttp Class

---

## Documenation Page?

Yes, it is on the way. Here is the github link:

https://github.com/Veams/veams

---

## Used in ...

- VW as alpha release
- BVMG with the latest release
- Auswärtiges Amt with latest release

---

## Questions?

![alt Questions](assets/img/questions-bale.gif "Questions")