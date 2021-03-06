# Reagent Selectors

Many methods in Reagent's API accept a *selector* as an argument. Selectors in Reagent can fall into
one of the following three categories:


### 1. A Valid CSS Selector

Reagent supports a subset of valid CSS selectors to find nodes inside a render tree. Support is as 
follows:

- class syntax (`.foo`, `.foo-bar`, etc.)
- tag syntax (`input`, `div`, `span`, etc.)
- id syntax (`#foo`, `#foo-bar`, etc.)

Further, reagent supports combining any of those supported syntaxes together to uniquely identify a
single node.  For instance:

```css
div.foo.bar
input#input-name
```

Are all valid selectors in reagent.  At this time, however, any contextual CSS selector syntax that
requires knowledge of a node's ancestors or siblings is not yet supported.  For instance:

```
.foo .bar
.foo > .bar
.foo input
```

Are all unsupported selectors in reagent.


**Want more CSS support?**

PR's implementing more support for CSS selectors will be accepted and is an area of development for
reagent that will likely be focused on in the future.



### 2. A React Component Constructor

Reagent allows you to find components based on their constructor. You can pass in the reference to
the component's constructor:

```jsx
class MyComponent extends React.Component {
  render() { ... }
}

// find instances of MyComponent
const myComponents = wrapper.find(MyComponent);
```



### 3. A React Component's displayName

Reagent allows you to find components based on a component's `displayName`. If a component exists
in a render tree where it's `displayName` is set and has it's first character as a capital letter,
a string can be used to find it:


```jsx
class MyComponent extends React.Component {
  render() { ... }
}
MyComponent.displayName = 'MyComponent';

// find instances of MyComponent
const myComponents = wrapper.find('MyComponent');
```

NOTE: This will *only* work if the selector (and thus the component's `displayName`) is a string 
starting with a capital letter. Strings starting with lower case letters will assume it is a CSS
selector using the tag syntax.
