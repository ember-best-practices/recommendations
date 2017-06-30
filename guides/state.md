## Reason about where state should live

As a general rule, state should only be mutated by its "owner". The owner is
location where the state was either originated (fetched/created) or derived.
By extension this also means that state should only be mutated at the same
level with the state tree at which it was created.
 
Manipulating or storing data at the incorrect locality often introduces
mutation backflow, potential memory leaks, issues with asynchronous teardown,
and unintentional and inconsistent side-effects. All of these scenarios can
adversely affect performance, code readability, and maintainability.
