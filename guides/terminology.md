## Terminology

### Mutation Backflow

Mutation backflow occurs when a child context mutates an object that is owned
by a parent context, causing changes in the parent context.  This is analogous
to "spooky action at a distance".
 
An example negative side-effect of mutation backflow occurs when a parent
component has already rendered when a child component mutates an object owned
or utilized by the parent component.  This forces the parent component to need
to re-render, and is one of several causes of what we refer to as a backtracking
rerender.

### Backtracking Rerender

A backtracking rerender occurs when already rendered data is mutated before the
entire render completes. This forces a second render pass to account for any
updated state. Backtracking rerenders are synchronous and will block paint.

### The State Tree

In a web application, state can live at many different scopes. We can represent
the scopes from outermost to innermost as a tree.
 
* Global State (state that is universal, would be true for any number of
  applications on the same window, such as in SSR or when running tests)
  * Application State (state that should live and die with the application
    instance, the application route and services fall into this category)
    * Route State (state that should live and die based on a route 
      activating / deactivating)
      * Local State (state that should live and die based on the display
        lifecycle of a single component, also known as "UI State" or
        "Component State")
 
You may notice similarities between the state tree and a DOM Tree. Because the
application has a root element, and routes nest as children within it, and
components and their subcomponents as children within routes, the DOM is a
reflection of the full state of the application.

### Data Down, Actions Up

"Data down, actions up" represents the philosophy through which state in the
state tree should be managed.
 
"Data Down" because data should be fetched near the top of the tree (at the
Application or Route level) and fed down to components.
 
"Data Down" also refers to yielding derived state out of a shared parent
component into multiple child components.
 
"Actions Up" because mutations to data should occur at the same level of the
state tree that owns or originated that data.  Components further down the tree
send an action back "up" the tree to the owner of the data signaling the piece
of data and the requested mutation.  For derived data this may be a parent
component.  For Application or Route level state the action should be sent to a
route or service.

### Sideways Communication

Sideways communication occurs either when sibling components communicate with
each other or when multiple instances of the same component communicate with
each other. 
 
Sideways communication is usually the result of two or more components sharing
the same instance of a mutable value such as a class, object or array via their
prototype, via a mixin, or via a service.
 
Like mutation backflow, sideways communication is analogous to "spooky action at
a distance", causing the app and it’s various parts to be difficult to reason
about and maintain.
 
Usually sideways communication leads to either unintentional or uncontrolled
mutation with a backtracking rerender as a consequence. It primarily leads to
highly inefficient change flow when many things depend on the value being
mutated.  Usually there is an optimal order and timing for reacting to data
changes and updating values, but when sideways communication is involved both the
order and timing are uncontrollable.

### Mutable Value

Mutable values are objects, classes, or arrays whose properties and/or methods can
be appended, deleted, or altered.

### Primitive Value

The opposite of a mutable value. Primitive values are immutable built in language
primitives such as strings, numbers, and null.

