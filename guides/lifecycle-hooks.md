## Prefer lifecycle hooks over lifecycle events

When building features or functionality that requires the use of the lifecycle,
lifecycle hooks are the preferred solution anytime the following are needed / required:
 
* Specific timing
* Specific ordering
 
By contrast, lifecycle events do not provide these features.  Also, when building a
base-class or mixin that implements a lifecycle hook, giving it a unique,
purposeful name is a recommended best practice, and will enable other engineers
to quickly understand and leverage that base-class or mixin if appropriate.
