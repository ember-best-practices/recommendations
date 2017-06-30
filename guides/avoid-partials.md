## Prefer Components and Helpers to Partials

Partials can often be difficult to reason about and maintain over time.  This is 
because there is no clear contract for a partials “this” context, and that can
result in unpredictable and counterintuitive behavior depending on the context.
This unpredictable behavior often makes partials difficult-to-impossible to
optimize by both glimmer and the browser. As an example, using partials within
an ‘each’ manifests this performance anti-pattern most consistently.
 
By contrast, components have a clear contract with the outside world, and should
be strongly considered as a favorable alternative when  reuse and composability
is desired.  Partials are not needed  to modify behavior from core within extended.
 
A better option for changing the entire layout of a component is to import a
separate layout and set it as the layout prop.
 
Better options for changing just a portion of the template of a component include:
 
* Utilizing the component’s `{{yield}}` to enable variable layouts
* Utilizing a component instead of a partial (and swapping out the implementation 
  of that component for one specific to extended or core)
* Utilizing the `{{component` helper with the name of a component
