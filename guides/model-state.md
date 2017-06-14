## Avoid Local/UI state on Models

Models live on the `store` service, and all services hold "application state."
UI or local state should not be entangled with application state by adding
it to a model.

Examples of UI or local state include:

* selection 
* focus 
* animation state 
* occlusion state
* information specific to the local display of a single component 
