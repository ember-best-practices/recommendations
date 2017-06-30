## Component Lifecyle Hooks

### Use the optimal lifecycle hook

Note: didRender and especially willRender are almost always the wrong hooks to use.

For a given component, these hooks will trigger every time the component, a
component used by its template, or a component within the yield re-renders.  This
is often more often than expected, is usually more often than needed, and can
occur multiple times for a single paint of the page.
 
For work that only needs to be done once on initial render, schedule the work
from `didInsertElement` (see discussion in the very next section).

For components that need to track a change on every paint, a scheduled task that
runs on each requestAnimationFrame is better. Such tasks should be rare and
it’s best to confirm whether there is a better approach first.

For components that need to check something in the DOM only after certain data
changes, scheduling work into `requestAnimationFrame` from `didUpdateAttrs` or
`didReceiveAttrs` ensures costly work is done only as often as needed and at
the right time.
