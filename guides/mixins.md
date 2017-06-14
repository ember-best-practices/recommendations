## Mixins

* Avoid creating and introducing new mixins when possible
  * For shared state consider using a service
  * For stateful functions consider using services or, very occasionally, helpers
* For stateless functions consider using shared functions (via utils, or helpers,
  or both)
  * Only fully encapsulated mixins (no mixins with abstract interfaces)
  * Avoid mixins that make specific assumptions about the types of objects
    they're mixed onto (i.e. don't implement didInsertElement, beforeModel or
    other lifecycle hooks for things such as components and routes in your mixin)
  * A great barometer is whether a mixin is unit testable by adding it to a regular
    Ember.Object.  If not, it's not "fully encapsulated".
* Avoid sideways communication via Mixins or services
* "Data-down-actions-up" is strongly recommended
  * Don’t mutate references being passed down
  * Don’t depend on mutation side-effects
