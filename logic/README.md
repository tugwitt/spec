# Logic Stack

the logic stack is far less defined, deliberately so. by definition, *we* do not control the logic stack; we merely use 
other people's logic stacks. at the end of the day, the issue with how we deal with data currently isn't the logic, it's
the fact that there's no such thing as a data stack.

basically, we'll just tap other people's backends. BSV and Urbit are the easiest examples, but it could be anything
that we can run general purpose code off of.

## Connectors

we're only going to have to write connectors for the logic stacks. meaning we'd just have to write a specific connector for a 
given method of executing compute across BSV, not rebuild BSV's backend.

the benefits of this are pretty clear, but this is the central idea behind backend sovereignty; if the backend we choose
dissapears tomorrow, the network shouldn't have a second of downtime.

the connectors really are nothing more than a way to run Atlas code off of that given backend. it will be closer to L2 interaction
than L1 directly, but there's not much more to it than that. all we need the logic stack for is to actually execute our code,
nothing more.
