# Store & Observable Patterns

--

## Sitemap

1. Introduction to Design Patterns
    1. Observer Pattern
    1. Publish & Subscribe Pattern
1. Problems with these Patterns
1. Data Ownership
1. Store
1. Observable

---

## Design Patterns

![alt Design Patterns](assets/img/design-patterns.gif "Design Patterns")

--

## Introduction

One of the best resources for JavaScript is <br>[Learning JavaScript Design Patterns](https://addyosmani.com/resources/essentialjsdesignpatterns/book/).

--

## Why patterns?

--

It is all about scalability, readability and a vocabulary to solve common problems.

> Patterns are not an exact solution. It’s important that we remember the role of a pattern is merely to provide us with a solution scheme.

--

## Typical problems in web applications are ...

--

- Asynchronous behaviour
- Communication between parts of the application
- Data Sharing
- ...

--

## How do we solve these problems?

--

By using patterns like ...

--

## Publish & Subscribe Pattern

![alt Design Patterns](assets/img/store-observable-pattern/pubsub-broadcast-design-pattern.png "Design Patterns")

--

## Observer Pattern

![alt Design Patterns](assets/img/store-observable-pattern/observer.png "Design Patterns")

--

## Comparison

![alt Design Patterns](assets/img/store-observable-pattern/difference-observer-pubsub.png "Design Patterns")

---


## Problems with these patterns

--

**Keep components loosely coupled while sharing data states is not as easy as it seems.**

--

**Furthermore you have to deep dive into the project to understand where the data is shared.**

--

**Moreover the developer decides which part of the application takes over a certain responsibility to modify the data.**

--

**The developer has to handle timing issues like binding events before publishing data by another event.**

--

**Open API can lead to an anti-pattern by using the pattern in a wrong way**

--

**To work with Pub/Sub systems needs conventions.**

--

**Data Mutation in components leads to different states and inconsistency.**

---

## Ownership of data

--

One of the main points you should ask yourself is:

**Which part of the application is responsible to modify and handle the data?**

--

That leads in general too a much cleaner application, because

1. Only one part is responsible to handle the data
1. Data sharing is accomplished by using this source

--

## Does that mean that a component can take over the ownership?

--

### Yes ...

You can do that by triggering actions which will be handled by the component.

--

### and no!

It leads to scalability problems, because now the component is responsible for things which are not covered by the component itself.

---

## Solution

**A centralized store as observable.**

--

The solution to solve a lot of issues is to use a centralized store which is an observable.

--

## What is an Observable?

```ts
export interface Observable {
    subscribe(obs);
    unsubscribe(obs);
}
```

--

## Jump in the code

https://github.com/aperto-frontend/store-observable-pattern

--

You can check out the branch `pubsub` to see `Veams.Vent` in action and how we implemented it.

--

You can checkout the branch `store` to see the improvements by using a `Store` class.

--

# Have Fun with part 1!

---

# Extend the base store

--

## Sitemap

1. Current state of the store
1. Requirements in the demo project
1. Get rid of the open api
1. Event dispatching
1. Update components
1. Data handling
1. Clean up

---

## Current state of store implementation

--

### What do we have?

1. A centralized store
1. observer/store pattern
1. a simple data object
1. a simple update method to add or modify data

--

### Problems

It does not fit into real world scenarios, because it is too simple for now.

##### Think about ...

--

### ... different data objects in your store.

--

### ... the open api problem in the Observer Pattern.

--

### ... the behavior how you would modify the data.

--

Let's keep that in mind and take a look at the requirements in the new demo project.

---

## Requirements in the Demo Project

--

### Status Quo

In the beginning we had two components:

1. Giphy List
2. Metadata View

--

### Next Steps (Expectation from the client)



1. Now we need to add an editor bar to delete that list and update the metadata view.
1. Furthermore a click on a list item opens up a popup.


--

### Do we need a discussion?

Do you want to talk about how you would do it in current projects?

---

# Refactor the store

--

## Open API

We want to get rid of the open api.

--

### Delete `initialize()`

--

### Exclude ...

- `broadcast()`
- `data`
- `dataSubject`

--

## Support event dispatching ...

... instead of using the public method `update()`!

--

### Create a `dispatch()` method.

--

### Add a simple `switch()` to that method.

---

# Update components ...

--

## ... by using the new `dispatch()` functionality.

---

# Refactor data handling ...

--

## ... by using multipe subjects.

--

## ... by using a simple store structure divided in `ui` and `data`.

--

## ... by extending our reducer*.

> The reducer is a pure function that takes the previous state and an action, and returns the next state.

--

## ... by adding a `select` function.

The `select` function is responsible for adding an observer to a specific subject.

--

## Hints

- Do not forget `break` in `case`.
- Broadcast to observers by using the `id`.
- Do not change the internal state of the component without updating the store.

---

# Veams Store Plugin?

--

Sure, there is now a simple plugin available. See https://github.com/Veams/veams-plugin-store.

--

## Usage

--

### Plugin Usage

``` js
import VeamsStore from 'veams-plugin-store';
import rootReducer from './store/reducer';
import INITIAL_STATE from './store/app-state';
import subjects from "./store/subjects";

Veams.use(VeamsStore, {
    reducer: rootReducer,
    state: INITIAL_STATE,
    subjects: subjects
});
```

--

### App State Structure

``` js
export default {
	data: {},
	ui: {
		overlayOpen: false
	}
}
```

--

### Subject Structure

``` js
import {Subject} from 'veams-plugin-store';

export default {
	data: new Subject(),
	ui: new Subject()
}
```

--

### Reducer Structure

``` js
import {state, broadcast} from 'veams-plugin-store';

export default function rootReducer(action, payload) {
	switch (action) {
		case 'DATA_GIPHYS_LOADED_ACTION':
			state.data = handleGiphysLoaded(state.data, payload);
			broadcast('data');
			break;

		case 'DATA_GIPHYS_CLEAR_ACTION':
			state.data = handeGiphysDeleted(state.data);
			broadcast('data');
			break;


		case 'UI_OVERLAY_OPEN_ACTION':
			state.ui = handleOverlayOpen(state.ui, payload);
			broadcast('ui');
			break;

		default:
			return state;
	}
}
```

---

# Have Fun

![alt Have Fun](assets/img/happy.gif "Have Fun")


