## System architectures

Described in terms of Modularity and Distribution

- Monolith - not modular, not distributed
- Modular monolith - modular, not distributed
- Microservices - modular, distributed
- Distributed monoilth - not modular, distributed

### n-layer monolith

Every team is working on the same codebase and can easily introduce side effects in unexpected places.
Deployed all at once.
Can have feature flags to turn of parts of system in given instance to allow for setting up multiple instances, of which only a few handle selected business processes.
Presentation layer, application layer, Data access layer; can have more layers, each dedicated to separate function.
Usually results from desiging the application based on database structure - table `User` is mapped to class `User`, which is then used by every process in whole system.
N-layer approach is very suitable for CRUDs when using microservices as system architecture, but here 2 layers might be enough - API and Data access. 
Extracting separate services is hard because there are no boundaries between separate modules of application.

### modular monolith

Separate teams can work on separate modules.
Can be scaled both vertically and horizontally.
Deployed all at once.
Can have feature flags to turn of parts of system in given instance to allow for setting up multiple instances, of which only a few handle selected business processes.
Modules communicate through defined ways and data contracts; one module never reference other modules internals.
Modules should also use separate data schemas, to avoid coupling on database level.

## misc 

Conway Law - communication and team structure results in system architecture looking similarly.

Constantine Law (?) - stable system have high cohesion and low coupling


