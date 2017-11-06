# Handlebars Breakdown

![alt Breakdown](assets/img/breakdown.webp "Breakdown")

--

## Sitemap

1. History
    - Problems and Alternatives
1. Handlebars out of the box
    - Problems and Solutions
        - Handlebars Helpers
        - Template Renderer Engine
1. Handlebars in Action
    - Typical Problems

---

# History

--

We started to use Handlebars in November 2013, because of:
- simplicity
- easy setup with Assemble
- great helpers
- no JavaScript knowledge
- logic-less templating

--

## There are also problems with that approach ...

- Inline variables cannot be set
- No logic at all
- For everything you need a helper

--

## Which alternatives are out there?

- [Jade](https://naltatis.github.io/jade-syntax-docs/)
- [Swig](https://github.com/paularmstrong/swig) | [Swig 2.0](https://github.com/node-swig/swig-templates)
- [Nunchucks](https://mozilla.github.io/nunjucks/)

You know anything else?

--

## What do you think, should we still use it today?

### What is your perfect template engine?

---

# Handlebars out of the box

It is a minimalistic template engine on steroids.

![alt Muscles](assets/img/muscles.gif "On Steroids")

--

## Do you know what comes out of the box?

--

- if, else, each, unless, lookup, log
- comments
- scoping
- partials

--

## Problems ...

--

### ... with helpers.

You only have a few helpers available.

--

### ... with a lot of additional work.

Everything needs to be added manually by you. There is no out-of-the-box setup.

--

### ... with a bad documentation.

Take a look at the website!

--

### ... with missing guides (best practices).

What is the right way to build scalable templates with Handlebars?

--

## Solutions ...

--

### ... for Helpers

- [Handlebars-Helpers](https://github.com/helpers/handlebars-helpers)
- [Handlebars-Layouts](https://github.com/shannonmoeller/handlebars-layouts)
- [Mangony-Hbs-Helpers](https://github.com/Sebastian-Fitzner/mangony-hbs-helpers)
- [Mangony-Hbs-Helper-Wrap-With](https://github.com/Sebastian-Fitzner/mangony-hbs-helper-wrap-with)

--

### ... for setups (Template Renderer Engine):

Template render engines are wrapper for template engines. They come up with a solution to provide a full eco system for layouting and data handling.

- [Assemble](http://assemble.io/)
- [Mangony](http://mangony.veams.org/)
- [Gulp-HB](https://github.com/shannonmoeller/gulp-hb)

--

## What is missing for you?

1. Where are improvements for your daily work?
1. Are there any problems by using Handlebars or one of the eco systems?
1. Do you have a wish?

---

# Handlebars in Action

![alt In Action](assets/img/in-action.webp)


--

## Data Mapping

With every partial you can use the data mapping feature.

```hbs
{{> c-image content=this.slider.references.image.content settings=this.slider.references.image.settings)}}
```

Pretty simple, right?!

--

## Data Merging

Sometimes you want to pass custom variables into the current context. Just use the `merge` helper.

```hbs
{{#merge this with='{"text": "lorem ipsum"}'}}
    <h2>{{headline}}</h2>
    <p>{{text}}</p>
{{/merge}}
```

Pretty simple, right?!

--


## Inline Helpers

You want to combine helpers? Really easy, just use `()` to execute a helper in another helper.

```hbs
{{#if (isObject references.image)}}
	{{> c-image references.image }}
{{/if}}
```

--

## Dynamic Variables Resolving

Perhaps you already know, that sometimes you have to recreate some JSON data in files where it does not belong to.

For example you have a `teaser` in which you are referencing another partial called `image`. Now you want to display a specific variation of that image.

**How do you do that?**

--

## Code Example

### Data

```hjson
"default": {
	"docs": {
		"variationName": "Default",
		"references": {
			"image": "default"
		}
	},
	"settings": {
		"teaserContextClass": "default",
		"teaserClasses": false
	},
	"content": {},
	"references": {
		"image": "default" // Reference to the variation object
	}
}
```

### Template

```hbs
{{> c-image (lookup @root.image-bp.variations references.image)}}
```

--

## Backend-Templates in Frontend?

**You know, you are a backend developer?**

You are writing backend templates which will be compiled to HTML. So what, if you want to use your backend templates in the browser, because you have some ajax content as JSON response?

--

## Just use Veams ;)

There is a plugin for that called `VeamsTemplater`.

---

## Questions?

![alt Questions](assets/img/questions-bale.gif "Questions")