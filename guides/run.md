## Usage of Ember.run methods

### run.schedule / run.scheduleOnce

Avoid usage of:

* `Ember.run.schedule('afterRender'`
* `Ember.run.schedule`
* `Ember.run.scheduleOnce`

This API exists primarily for ordering work at an extremely low level within
Ember itself. Instead of using `afterRender`, use didInsertElement which has
a guarantee that all DOM construction has completed.
 
Using `'afterRender'` to avoid a `"you modified X twice in a single render"` error
means the underlying cause for modifying X twice should be investigated and fixed,
as this is likely a serious performance issue in the component. While the error
goes away, this introduces a backtracking rerender.
 
Using `afterRender` to mean either "after the browser has painted" or "before the
browser paints" was not the intention of the API hook, and is almost always not
the optimal solution for this particular use-case.  Work done here will delay render.
 
Using `afterRender` from within a Route to mean "after Ember has rendered this
route" is not the intended use of the API hook since there is no guarantee that
the route will have rendered before the callback is executed.
 
For 'once' behavior when scheduling a DOM read or write, use a local variable to
track whether you have scheduled and flushed.

### run.next

Avoid usage of `Ember.run.next`.

This method defers some work via a call to `setTimeout`, which introduces a race
condition between when this work will be done and when the browser will paint.

Using `run.next` to avoid a, `you modified X twice in a single render` error
means the underlying cause for modifying X twice should be investigated and fixed,
as this is likely a serious performance issue in the component.

There are a few situations in which deferring via a `setTimeout` is desirable, but
overwhelmingly these situations need careful coordination.

