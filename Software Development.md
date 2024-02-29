# Software Development+

- In simpler examples, it’s usually easier to go top-down, and on larger projects, it’s easier to go bottom-up.

- Single responsibility principle (**SRP**), a component should ideally only do one thing, has therefor only one reason to change.

- Don't repeat yourself (**DRY**), Every piece of knowledge must have a single, unambiguous, authoritative representation within a system. Whenever a software system must support a set of alternatives, one and only one module in the system should know their exhaustive list.

## Projektmanagement

- Scope Creep [link](https://en.wikipedia.org/wiki/Scope_creep)
  - Have your Projectscope boundaries fix and propely deifnedfrom the biginning
- Feature Creep [Feature](https://en.wikipedia.org/wiki/Feature_creep)
  - Keep your feature arround the core idea, dont bload


## PURE CODE

- Pure functions don’t mutate variables outside of the function’s scope or objects that were created before the call, they have no side effects
- It minds its own business.
  - It does not change any objects or variables that existed before it was called.
- Same inputs, same output.
  -  Given the same inputs, a pure function should always return the same result.
-  **local mutation**, it’s completely fine to change variables and objects that you’ve just created inside the function while calling it