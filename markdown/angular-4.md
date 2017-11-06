# Angular 4 - Introduction

--

## Sitemap

1. General Structure
2. Angular Cli
3. Module
4. Component
5. Service
6. Provider
7. Dependency Injection
8. Route
9. Template
10. Directive
11. Pipe
12. Interface
13. Decorator
14. `implements`

---

## General Structure

The core of Angular is written in TypeScript, means we have a programming languages which supports types, interfaces, classes and more.

#### Important Notes:
- Angular uses Decorators (Component Decorators, Property Decorators, Method Decorators)
- You do not extend core classes, you implement interfaces (no inheritance)
- You use the constructor to provide services

---

### Angular-Cli

Angular now comes with a command line interface (CLI) to make it easier and faster to build Angular applications.
We will use it as our main instrument to scaffold blueprints.

--

### Installation

``` bash
npm install -g @angular/cli
```

---

## Module

A module is a complex setup which you want to provide to your application (for example a framework)
``` js
@NgModule({
    imports: [
        CommonModule,
        RouterModule
    ],
    declarations: [
        BodyComponent,
        ContentComponent,
        TitleBarComponent,
        StatusBarComponent,
        MainNavComponent,
        NavItemComponent
    ],
    providers: [
        FrameworkConfigService,
        ScreenService,
        MenuService
    ],
    exports: [
        FrameworkBodyComponent
    ]
})
```

---

## Component

--

Components are the fundamental building block of Angular applications.

Components are composable, we can build larger Components from smaller ones.

An Angular application is therefore just a tree of such Components, when each Component renders, it recursively renders its children Components.

---

## Service

--

A service contains functionality which helps us in structuring & providing and getting data, see also provider.

---

## Provider

--

A provider configures injectors by linking a token to a dependency.

![alt Funny](assets/img/questions-bale.gif "Funny")

Get in touch with Dependency Injection ;)

---

## DI (Dependency Injection)

--

### What is a dependency?

When module A in an application needs module B to run, then module B is a dependency of module A.

--

### What's wrong with the code?

``` ts
class MailChimpService extends EmailService { }

class EmailSender {
  emailService: EmailService;

  constructor() {
    this.emailService = new MailChimpService("APIKEY12345678910");
  }

  sendEmail(mail: Mail) {
    this.emailService.sendEmail(mail);
  }
}
emailSender = new EmailSender();
emailSender.sendEmail(mail);
```

--

### Clean Up

``` ts
class MailChimpService extends EmailService { }

class EmailSender {
  emailService: EmailService;

  constructor(emailService: EmailService) {
    this.emailService = emailService;
  }

  sendEmail(mail: Mail) {
    this.emailService.sendEmail(mail);
  }
}
emailSender = new EmailSender(new MailChimpService());
emailSender.sendEmail(mail);
```

---

## Template

--

A template is a simple html file which contains your markup with sugar (`ng-`) on top.

---

## Directive

--

Directives are components without a view. They are components without a template. Or to put it another way, components are directives with a view.

We typically associate directives to existing elements by use attribute selectors, like so:

``` html
<elemenent aDirective></element>
```

---

## Pipe

--

Pipes are used to transform data, when we only need that data transformed in a template.
We use a pipe with the | syntax in the template, the | character is called the pipe character, like so:

``` hbs
{{ 1234.56 | }}
{{ 1234.56 | currency : 'USD' }}
```

---

## Interface

--

An interface is simple object which provides a predefined structure. For example:

``` js
export interface IconFiles {
    imageFile: string,
    alt: string,
    title?: string,
    link: string
}
```

Here you can see that title is an optional element.

---

## Decorator

--

A decorator "extends" the object with metadata. There are two decorator types:
 - Component Decorator: It is the main decorator which you will use most of the time to extend a specific class with metadata.
 - Property Decorator: This is splitted up into method and property decorator. Usage can be`@Input`, `@Output`, `@HostListener`.

---

## `implements`

--

Implements are always used in angular to enrich the specific class you are creating. Like it said, it implements an interface.
In comparison to react or other systems it does not extend a base class. Therefore it does not have any inheritance in place.