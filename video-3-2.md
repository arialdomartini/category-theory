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


## Kleisli Category
Suppose we have a program and we have to add this new requirement:

* Every function must create an audit-trail

The simplest solution is to use a global log, for example something that is a string:

```cpp
string log = "";

bool negate(bool x) {
    return !x;
}
```

We modify it as:

```cpp
string log = "";

bool negate(bool x) {
    log += "not!";
    return !x;
}
```

This should be repeated for every single function. What's wrong with this solution? Is simplicity measured in the number of lines of code? Complexity and simplicity are not a simple topic. Simplicity is not easy: it needs to be simple, but it's not necessarily easy.

If we do this, we introduce something that is not immediatily visible from the code, but that increases the complexity of the system: there's a hidden dependency between functions and the global log, a long distance interaction.

This would for example impede the use in multi-threading environment. The next logical, simple solution would be to use a global lock.

Locks don't compose, we can have possible deadlocks.

In Haskell this wouldn't happen because it forces functions to be pure. So the question is: how to get to the same result using only pure functions?

A possible approach is:

```cpp
pair<bool, string> negate(bool x, string log) {
  return make_pair(!x, log += "not!);
}
```

Everything is pure, no side effects.

This is awkward. The function is pure, because we can memoize. But now meoization is very complex and very consuming. The original function was easy to memoize.

A second problem is the function knows something it does not belong. Why does the function know about appending strings? We are violating the principle of separation of concerns. It's a good solution, but not quite.

Let's try to remove the need for the function to know about appending strings.

```cpp
pair<bool, string> negate(bool x) {
  return make_pair(!x, "not!);
}
```
Now the function only does its own things. Who does the appending of this log, now? 

What do we do with functions? We compose them. So, we need to be able to compose functions like this with a modified process of composing which includes appending strings.

Let's start from the regural composition `g . f`

```cpp
function<C(A)> compose(function<B(A)> f, function<C(B)> g) {
    return [f, g](A x) {
        auto b1 = f(x);
        auto c1 = g(b1);
        return c1;
    }
}
```

In C#:

```csharp
Func<A, C> Compose<A, B, C>(Func<A, B> f, Func<B, C> g)
{
    return new Func<A, C>(a => {
        B b1 = f(a);
        C c1 = g(b1);
        return c1;
    });
}
```

in Haskell:

```haskell
compose :: (a -> b) -> (b -> c) -> (a -> c)
compose f g a = g ( f a)
```

With pairs:

```cpp
function<Pair<C,string>(A)> compose(function<Pair<B, string>(A)> f, function<Pair<C, string>(B)> g) {
    return [f, g](A x) {
        auto b = f(x);
        auto c = g(b.first());
        return makePair(c.first(), b.second() + c.second());
    }
}
```

In C#:

```csharp
Func<A, (C arg, string log)> Compose<A, B, C>(
            Func<A, (B arg, string log)> f, 
            Func<B, (C arg, string log)> g)
{
            return new Func<A, (C, string)>(a =>
            {
                (B arg, string log) b = f(a);
                (C arg, string log) c = g(b.arg);
                return (c.arg, b.log + c.log);
            });
}
```

This is a new way of composing functions which takes care of appending strings.

It is associative, because string concatenation is associative. Identity is

```cpp
Pair<A, string> id(A a) {
    return makePair(a, "");
}
```

```csharp
Func<A, (A, string)> Identity(A a) => (a, String.Empty);
```

We have a binary operator `+` and a unity `""`. It works for any monoid, not only with strings. Instead of defining this combination for string, we could impose as few constraints as possible and define it for any monoid.
