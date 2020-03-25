Kleisli Category
================

## Example
Let's define the relation *inclusion* on Sets, to be a subset of a given set. Is it an order, or a pre-order? What should we check?

* Does it have identity? *to be subset of itself* is the identity
* composibility: `a subOf b, b subOf c => a subOf c`
* associativity

It's a pre-order.

It's also a partial order: there are no loops: `a subOf b && b subOf a => a = b`.

It's not a total order: there are sets that are totally disjoint.

It's possible to have a diamond: `a subOf b, a subOf c, b and c subOf d` and `b, c` are unrelated. It's like in a Venn diagram.

