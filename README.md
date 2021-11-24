# View Component Design Pattern <!-- omit in toc -->

A simple design pattern for JavaScript frontend development. The goal of this design pattern is to provide a technique to build applications or widgets with view components that encapsulate UI state while keeping the pattern as simple as possible.

---

## Copyright <!-- omit in toc -->

© Jake Knerr at Blotli.

---

## Table of Contents <a id="toc" name="toc"></a> <!-- omit in toc -->

- [View Components](#view-components)
- [API](#api)

## View Components

For this document, the term "component" refers to a view component.

#### UI state represents the totality of the user interface state for a group of components as a whole.

The group of components could be an application or a complex aggregate component.

#### UI state can be broken into smaller parts that are individually known as simply _state_. In this document, _state_ refers to a part of UI state.

#### UI state is presented via a group of components, with a single root component parenting a tree of child components.

All components have a parent component, with the only exception being the root component.

This tree of components is referred to as the "component tree".

#### Each component may have its own internal state, controller code, and a view.

Components are MVC components.

#### A component's view is its state representation, its reflection of state to the display.

#### All components are required to have a view.

#### Parent components manage the state of child components. They pass the child component state and they modify their child components' state.

Components do not directly modify the state passed to them by a parent component. Components may manage their own internal state, but the state that is passed to them is managed by their parent.

#### Parent components handle the process of adding child components to themselves. In other words, components do not add themselves to the component tree.

This includes adding a component's view to the display. A parent component adds a child component's view to the display.

This does not necessarily mean that the parent's HTML is the parent element for the child's HTML. For example, assume a child component has a modal view. The modal view is parented by `document.body`, not the parent's HTML. Thus, the parent's view does not strictly parent the child's view. Rather, the parent component is responsible for adding the child's view to the display.

However, typically a parent component's HTML will be the parent element for child component HTML.

#### Components do not need to know anything about their parent component.

#### A component should only change state if it manages that part of the state.

A particular state should be managed by the component that is (1) closest to where the state is _used_ and also (2) parents all the other components that use the state. This way, if the component managing state mutates said state, it can handle sending the updates to all of the children who depend on the state.

Note that what matters is where the state is _used_. State may be stored higher up in the component tree, but it is where it is actually used that counts when determining what component can mutate the state. For example, data may be stored on the root component, but where it is used determines what component manages it and can mutate it.

#### Updates flow from component to component in a top-down, parent to child manner. Don't skip the line without a good rationale.

It's easy to reason about this unidirectional system.

#### Parent components can handle state changes in children by passing callbacks into child/grandchild components. The passed callbacks can be called by child components to return state management back to the parent component.

#### All component names are nounal.

Components are things, like nouns.

**[⬆ Table of Contents](#toc)**

---

## API

#### Components wrap an HTML element.

#### Each component exposes the `$` property as a reference to the wrapped HTML element.

#### External code can interact with the view's `$` property.

In other words, the `$` property is public. This prevents creating redundant wrapper code to interact with the DOM element when the DOM already provides an extensive API.

**[⬆ Table of Contents](#toc)**

---