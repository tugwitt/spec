# Stack Heirarchy

as of now, we have a three layer stack:

- [assembly](./layer1.md) (**layer 1**)
- [compiler](./layer2.md) (**layer 2**)
- [interface](./layer3.md) (**layer 3**)



## Layers

### [Assembly](./layer1.md)

our assembly layer is really just a base language ([Atlas](http://liegroups.org/software/documentation/atlasofliegroups-docs/tutorial_with_examples.html))

### [Compiler](./layer2.md)

our compiler layer is mostly a query parser, tokenizer, and validator

### [Interface](./layer3.md)

our interface layer is the layer most users will touch; it's the interface to actually update our database