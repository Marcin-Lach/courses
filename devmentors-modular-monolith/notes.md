# Modular monolith by DevMentors

Link to course - <https://platform.devmentors.io/courses>  
Link to codebase - <https://github.com/devmentors/Confab>


## chapter 1 - Application and system architectures

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

Conway Law - "Any organization that designs a system
(defined broadly) will produce a design whose
structure is a copy of the organization's
communication structure."

Constantine's Law - "A structure is stable if cohesion is strong and coupling is low."


## chapter 2 - software analysis, event storming

Should involve business people, domain experts and programmers.
Meeting facilitator should be present to keep the meeting on track.
Facilitator should identify discussions, that should be postponed, mark places with hot spot and stick to the schedule.
Everyone should be active and feel comfortable, participating in discussion about problem and solution.
If meeting in person, room should be designed to make cooperation and communication easier - big wall for sticker notes, chairs removed, so that people do not hibernate on them.

### es - main levels
- Big picture - learning about business, defining processes, getting knowledge from domain experts
- process level - going deeper into a single process but still from business perspective
- design level - mapping business process to programming solution

### es - sticker note types

- orange - domain event, something that happened and can be reverted only by additional domain events; should be focused on events important from business perspective - fetching data from DB will in most cases be not important, but events such as "approved order", "received payment" will most probably be important
- yellow - actor - person interacting with system
- red - hot spot - a point in system that is worth paying attention to (such as any problem, unclear domain) 
- pink - external systems (such as payment processor)

- violet - policy, some more complicated process, which can go in a few different ways
- dark yellow - (on design level) aggregate in DDD meaning
- green - (on design level) read model, any data fetched from system
- blue - (on design level) command - any intention of actor or external system, that leads to a change in system (command usually results in domain event)
- green - opportunity for improvement in system, usually around hot spots
- violet - voting card - after big picture, decide which hot spots and opportunities to take into work scope as first

Colors of sticker notes can be adjusted to personal needs.

### es - big picture - conducting

Introduce people gradually into sticker note types, starting only with orange (domain events).
People can feel scared to add first sticker notes to board.
If people are paralyzed, facilitator can add first sticker note to the board.
To make everyone comfortable, be supportive. If someone names domain event in present tense, do not immediatelly correct them (it should be in past tense, as something that has already happened).
This is the moment to identify domain language (DDD nomenclature - ubiquitous language).
Can bring up ideas forhow things can be implemented, but it is not the meeting where implementation should be discussed, leave it for Design Level meeting, where less business people will attend.

#### es - big picture - phases
 
First phase is chaotic exploration. Everyone should just spam with domain events for first ~20mins (until no new sticker note is added).
Afterwards, put a timeline (leftmost is oldest) on top of notes and try to order notes chronologically.
Group notes with similar names close to eachother.
Add swimlanes to separate processes from eachother.
Mark pivotal events - events that looks like they are very important, events that clearly separate one process from another.
Hot spots (red cards) can be added.
External systems (pink cards) can be added.
Actors (yellow cards) can be added.

### es - process level

Do not grab nouns and use them as module names.
Try to focus on identifying processes and grouping events in a way that limit communication between modules.
It can become a bit intertwined with design level, you might see aggregates, bounded context etc.