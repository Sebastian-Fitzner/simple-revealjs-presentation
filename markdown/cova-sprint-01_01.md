# Goals for Sprint 1 - Week 1

--

## Sitemap

1. General Setup
1. i18n with Poolswift or Transiflex
1. Observers & Observables
1. Reactive Forms
1. Further Terms

---

## General Setup

First of all we need to finalize the general setup. This contains multiple elements like `header`, `footer` & `navigation`.

Next to these we need to rename `fw` to `bb`. That way we have the same terms over all of our projects.

--

### Navigation

I already setup the navigation component in the building-blocks area. The service for the navigation should be added as well.

It is important that the service also stands in the building-blocks section and that you will get familiar with dependency injection.

---

## i18n

We will get a decision today which tool we are going to use.

Both tools leads to a different approach how we will handle i18n in the project.

--

### Poolswift

--

#### Translation Groups

We should group the translations into sections which are understandable for the content editor, means

- Dashboard
- Login
- Register

It is more connected to the general UI than to the technical components.

--

#### Handling

We have already our API endpoint, so why shouldn't we use it?!

Therefore we just create an i18n service which gets the full translation.

This service will later be injected as dependency:

``` typescript
export class MainNavComponent implements OnInit {
    i18n: any;

    constructor(private i18nService: I18NService) {
        this.i18n = this.i18nService.get('general');
    }
    ...
}

```

--

### TransiFlex

--

#### Handling

TransiFlex returns a file which you need to save in our repository.

Every time when there is an updated version out there it needs to be updated in our repository as well.

It is a XML file which we need to convert to JSON.

Last but not least we have a local file which we then use as endpoint.

---

## Observer & Observables

In this sprint we need to get in touch with `RxJS` to understand how we can handle all asynchronous tasks with `Observers` and `Observables`.

Every service which has data in it should be an `observable` stream.

--

### A short Definition

ReactiveX is a combination of the best ideas from the Observer pattern, the Iterator pattern and functional programming.

You create event or data streams, compose and transform the streams (functional programming part) and subscribe to that observable (observer pattern).

---

## Reactive Forms

Reactive forms is an Angular technique for creating forms in a reactive style.

There is a guide: https://angular.io/docs/ts/latest/guide/reactive-forms.html

--

### Dynamic Forms

For this week we should think about creating a dynamic form component. The main goal is to achieve something similar to `JSON Schema Form`:

- Data Service and View Model (JSON Schema)
- Dynamic Form Component
- Dynamic Field Component with Widget-Support (JSON UI Schema)
- Generated Forms (Create, Read, Update)
- Observable Based Forms with Validation and Error Handling

---


## Further Terms

--

### Angular Compiler

An Angular application consists largely of components and their HTML templates. Before the browser can render the application, the components and templates must be converted to executable JavaScript by the Angular compiler.

We have two compiler options:

1. JIT (Just-In-Time)
2. AOT (Ahead-Of-Time)

We are going to use the AOT approach in our production build, so we kick out compilation time on runtime by using the angular compiler in our bundle process.

That means that we speed up the general compiling of JavaScript in the browser.

--

### Content Transclusion

Here a short definition:

> Content Transclusion means that you can define placeholders `<ng-content>` which get replaced by other content.

Think of it like our `wrapWith` helper with less power ;)!