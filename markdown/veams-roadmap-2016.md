# Veams Roadmap

--

## Sitemap

1. What have we done in the last two month?
2. What can be used now?
3. Upcoming tasks
4. Preview of Veams 5

---

### What have we done in the last two month?

![alt Boring](assets/img/work.gif "Work")

--

### Veams Generator (v7.6.1)

- Replaced grunt-contrib-watch with grunt-chokidar
  - _better performance, cpu usage is lower_
- Updated packages
- Updated grunticon
  - _supports embeding of svg icons via JavaScript_
- Updated blueprint templates
  - _new structure in the data and handlebars files_
- Added new Veams-JS version 4
- Added icons webfont
- Added new media mixin lib
- Added Veams-Query
- Added self-contained component option
  - _it is also a default setting_
- Added stylelint

--

### Veams-JS (v4.x)

- Updated all external libraries
- Added Veams-Query support
- Improved event handling in app.js
- Added lazyloading for images as default
- Added ajax handling with custom option delegation
- Replaced respimg.js with picturefill.js

---

# Veams Components

We refactored almost every component. Now they ... 
- ... have a new structure.
- ... are completely self contained. 
- ... are documented with various variations.
- ... have a nice README file.

--

## The New Structure

The new structure is visible in the data and template files. But you can also see some minor changes in the SCSS files.

--

## Templates and Data


The new data and template structure divides settings from content. With that in mind you make the component easier to read und nicely structured.

``` json
"variationName": {
    "settings": {
        "quoteContextClass": false
    },
    "content": {
        "quoteContent": "Lorem ipsum dolor sit amet ...",
        "quoteAuthor": "– Albert Einstein –"
    }
}
```

-- 

## SCSS

In our SCSS files we support global default variables for each component. 

These can be overridden by using the variable in your `_vars.scss` or just by changing the value in the file itself. 

``` scss
// General
$slider-darken: 10 !default;
$slider-unresolved-height: 300px !default;
// Animation Variables
$slider-duration: 600ms !default;
$slider-ease-method: ease !default;
// Controls
$slider-control-bg-color: #a5cfd1 !default;
// Pagination
$slider-pagination-color: #555 !default;
$slider-pagination-color-active: $slider-control-bg-color !default;
$slider-pagination-size: 15px !default;
$slider-pagination-border-radius: 25% !default;
```

-- 

## Demo Page?

Yes, it is on the way. We only need to add a nice front page, but here you can see a preview: 

http://new-examples.veams.org/

---

## What can be used now? 

![alt Use it](assets/img/use-it.gif "Use it now")

--

###  Veams-JS, Veams-Generator, Veams-Cli

-- 

### Veams Components

Every updated Veams Component starts with the major version 2.xx.

-- 

### Blueprints

If you scaffold a new type (component, block, utility) into your project, you will get the new structure as well.

-- 

## Documentation 

You can use the documentation boilerplate for mangony. That means, everything is documented automatically by generating pages for your components. 

The components documentation page is a good example.

--- 

## Upcoming Tasks

![alt Tasks](assets/img/tasks.gif "Upcoming tasks")

--

- Some components are not ready yet, in example: form, sticky, dropdown
- Add scaffold process for the automated documentation
- Veams 5

---

## Veams 5 Preview

The goal of Veams 5: 

1. Provide a real framework
2. Concatenate Veams-JS and Veams-Sass

-- 

## Example

In Volkswagen we are already using Veams 5. Let's have a look.

---

## Questions?

![alt Questions](assets/img/questions-bale.gif "Questions")