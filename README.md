# spec
spec for something nameless

this is pretty much a dual stack implementation of generalized networks. we assume two stacks, the data stack and the logic stack. the data stack is to be built in house. the logic stack is variable and can tap into any valid backend, provided we have the proper connectors (AWS, BSV, urbit).

## Base axioms

- prioritize calculating the ODE instead of summing all PDE's
- maintain backend sovereignty
- maintain isomorphism across states overtime
- maintain [ACID](https://en.wikipedia.org/wiki/ACID) DBMS standards


### General Network Structure

the base idea is that we are the network. we own the outer network, SubNet Main. we have a more robust network manager on our outer layer. each subnet on our network than has the same base structure (data, logic, manager) but can be varied for the requirements of that specific network layer (i.e. user, customer, company, 3rd party, etc). 

### General Structure for an Arbitrary Network Layer

**just defining the top layer of the network**

there are really three components:
- [data stack](./data/)
- [logic stack](./logic/)
- [middleware/network manager/OS](./manager/)

#### Data Stack

the data stack is really nothing more than a base implementation of a Lie database. our base layer for this is the Lie group package de recommended, [Atlas](http://liegroups.org/). we will most likely build the second and third layer (and really layer 1.5 as well). 

#### Logic Stack

the logic stack is nothing more than a pool of compute to use. we just need to start with one backend, but here's the basic idea for what the connector looks like per backend:

- *AWS (custom server)*:
  - this will look like a lightweight node running on a server. it's really just a node that can run Lie algebra's on a given server (lang doesn't really matter here). probs our initial implementation. 
- *Urbit*:
  - this will look like an API connector that connects to a given Urbit planet/ship. 
- *BSV (any chain)*:
  - this will look like an API connector running off Planaria that allows you to pay for compute on the BSV chain from a given wallet
  
#### Manager

the manager is almost like the backprop agent. it's the thing that's *using* the compute from the logic stack to update our implementation of the data stack (i.e. a new 'row' comes in to be inserted, the manager uses the AWS connector to update the specific Lie group representation for that dataset). the manager can be a kafka agent for starters
