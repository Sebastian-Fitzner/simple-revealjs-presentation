# Technical Documentation

--

## Expectation

- fully automated
- no performance problems
- easy to configure

--

## Is it possible?

Not quite ... 

![alt Sad](assets/img/sad.gif "Sad")


-- 

... but we are fairly close.

![alt Happy](assets/img/happy.gif "happy")

--

## Demo Time

-- 

## How do we achieve this? 

Therefore we need to take a look into our template engine. 

---

# Template Engines 

--

## Status Quo with Assemble

Overall Assemble is pretty nice! We have: 
- Handlebars
- Many helpers (+130)
- Static files as deliverable product
- Markdown and data support

--

## What's the problem?

1. Compilation time of many files
2. Assemble uses an outdated version of Handlebars
3. `grunt-assemble` is buggy 
4. An automated technical documentation is not easy to solve (see 1.)
5. Grunt specific

---

# How do we solve these problems?

With the new kid on the block: 

--

<img width="400px" src="./assets/img/logo.svg" alt="Logo Mangony" />

_Think of Assemble ([grunt-assemble](https://github.com/assemble/grunt-assemble)) with a smooth mango juice - yummy._

--

## What can you expect?

1. Usage in Grunt, Gulp or standalone. 
2. By using the provided development server ([express](https://github.com/expressjs/express)) every change is completed in no time, no matter how many pages you have in your project.
3. Only changed pages get compiled. 
4. Creation of deep ids is possible for all types. 
5. For every type (data, partials, layouts, pages) Mangony adds its own watcher ([chokidar](https://github.com/paulmillr/chokidar)).
6. [HJSON](https://github.com/laktak/hjson) is available.
7. [Handlebars](https://github.com/wycats/handlebars.js/) version 4.x is integrated.
8. Markdown pages with handlebars are supported.
9. Internal caching.

--- 

# Benefits for the coder?

--

### Performance

Internal caching and a development server boost the overall performance. 

**Every change completes in no time (milliseconds)** 

-- 

### Helpers & Handlebars

- `@root` helper: Just go to the root context - nice!
- Data mapping on partials `{{> test data=this.items}}`
- more Helpers

-- 

### Data handling 

- `HJSON`: just comment in your JSON files - pretty kewl.
- Markdown with attribute support. 
- `contextData` as YFM: You can provide a specific data object for your page. 
- `currentPage` object with metadata for the current page.

-- 

###  What else?

- API communication possible (express server).
- It is stable.
- It has tests.

-- 

## Is there a project?

- Denn's 
- MometaHEXAL

--

### Great, isn't it?!

![alt Magic](assets/img/magic.gif "Magic")

--- 

## What is changing? 

Nothing at all, if you use `{{#block}}` and `{{#extend}}`. 

If you use layouts in YFM, `{{> body}}` needs to be replaced with `{{{yield}}}`. 

---

## When can we use it? 

Til friday there will be a documentation boilerplate which can be scaffolded. 

The usage of a technical documentation is already possible. 

-- 