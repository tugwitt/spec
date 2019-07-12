# Manager

the manager is our central controller. this is the system that maintains the equilibrium of the network (via fluid dynamics).
the initial implementation will probably be Kafka.

so this module has two real pieces: 
- the event controller ~ [Kafka](http://www.vldb.org/pvldb/vol8/p1654-wang.pdf)
- the network manager ~ [a (custom) ZeroTier offshoot](https://arxiv.org/pdf/1203.5026.pdf)

eventually, these two *will* merge into one module; we're doing this to avoid building a custom Kafka implementation right now.

## Event Controller

the event controller is what deals what routes jobs, handles scheduling, handles logging, etc. this will begin as
an implementation of Kafka, which is our distributed processing. 

if our [filesystem](../data/filesystem/) is just a basic heirarchical filesystem, the aspect that matters is the controller
that modifies that filesystem. so there are two pieces its keeping track of - the `general Lie group` of the dataset and 
the `commit log of records`. 

### General Lie Group

this is the representation of the underlying "model" of the dataset. initially (before any data is inserted), this will start out as some base representation.
this state model gets updated as new data is inserted through a kind of "backprop" (the [Lie derivative](https://en.wikipedia.org/wiki/Lie_derivative)). this is meant to be the general representation of a given dataset, in the same way the e8 Lie group is the general representation of particle physics. 


### Record Commit Log

maintaining isomorphism over time (meaning you can always traverse back to previous states) is a requirement. so each record
gets represented as a "partial Lie group", which is really a [manifold](https://en.wikipedia.org/wiki/Manifold) that represents a subset [subgroup] of the General Lie Group. even if the General Lie Group isn't fully defined, the manifold is *still* a 
representation of *the* General Lie Group. 

these manifolds can be represented as an `Atlas` subquery of the General Lie Group. this means the filesystem would have the 
General Lie Group .at file as the root of the heirarchy, and all states would be .at files representing queries across that
General Lie Group.


## Network Manager

this handles the `SubNet Main` network and all resulting subnets. this is the system that *creates* a subnet for a user
and manages the equilibrium within each actual subnet. 

the network manager acts as our centralized processing unit, as well as the maintainer of the network (though maintenence may end up being a parent module). this does the heaviest computations that are done at relatively predictable [non-instantaneous]
rates compared to the rate of records being updated. the distributed processing handles the smaller, instantanous logic.

the fundamental difference between our approach and the [approach](https://arxiv.org/pdf/1203.5026.pdf) Xu et al. took is that
we aren't focusing so much on the equilibrium as the fact that the degree of centralization *can* be varied. the reason the 
equilibrium component comes in is when you want to optimize the system to utilize the centralized compute when it's
being underutilized elsewhere, and vice versa. 

the network manager also must have logic for creating subnetworks, spawning a sub-manager to manage that subnetwork, 
and managing the parent child relationship between all managers. 


