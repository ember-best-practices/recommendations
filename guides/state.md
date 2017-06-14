## Reason about where state should live

As a general rule, state should only be mutated by its "owner". The owner is
location where the state was either originated (fetched/created) or derived.
By extension this also means that state should only be mutated at the same
level with the state tree at which it was created.
 
Manipulating or storing data at the incorrect locality often introduces
mutation backflow, potential memory leaks, issues with asynchronous teardown,
and unintentional and inconsistent side-effects. All of these scenarios can
adversely affect performance, code readability, and maintainability.

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
