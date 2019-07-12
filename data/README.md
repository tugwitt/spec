# Data Stack

so the data stack is just the system we use to store and update our data. we have our base layer, [Atlas](http://liegroups.org/software/documentation/atlasofliegroups-docs/),
as essentially our assembly. the layers above are abstractions to make running the base Atlas code easier.

## [The Stack](./stack/)

### [Layer 1](./stack/layer1.md)

Atlas is basically just a scripting language for Lie groups. it can run on a separate Docker container but eventually we'll want
to integrate the compiler ourselves. though it handles the interpreter as well, it's best to think of this as the *assembly layer*.

### [Layer 2](./stack/layer2.md)

the second layer is really just an API that allows you to run code through our Atlas compiler system (in a language, i.e. via Python).
this is pretty much the *compiler layer*. 

### [Layer 3](./stack/layer3.md)

the third layer is where user interaction takes place. this looks like robust API's in many languages that allow you to query
and update the actual database [filesystem]. this is pretty much the *full language layer*.


## [The Filesystem](./filesystem)

though the stack solves most of our problems, we still have to have a place that we store our actual data in.
this is the most unclear part as of now, it's most likely going to be a rough filesystem to begin with.

the easiest way to think about it is that anytime you want to update the database [filesystem], the data is "inserted" [sent to the manager],
the manager uses the existing data representation [Lie group of the dataset] and the logic stack [compute pool] to figure out
what to change in the filesystem and executes the change. 

this is getting very very similar to [atomic transactions](https://en.wikipedia.org/wiki/Atomicity_(database_systems)) in databases.
