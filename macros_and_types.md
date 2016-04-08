From Romeo:
  Term types specify binding information. If a binding relationship is broken, all hitherto bound names become free, and in the process must be freshened.
  Names have meanings relative to other names in environment (of the metaprogram), which is weird, but works.
  
Term types look like, say, `Expr<Integer>` or `Var<Fn<Integer, String>>`. Note that `Expr<Integer>` may have free names in it! It is possible to emit code with unbound names, which will not be executable, but if names *are* bound, we know their values will ultimately have the same type that they were constructed with.

What are the types of common syntactic forms? For the moment, I'm leaving off binding information. Is it expressible in a reasonable way without having to add a purpose-built type feature? Perhaps the lesson from Redex is that binding information need not reside in the type at all; it is safe for it to reside in (and even depend on!, we hypothesize) the value.

```
lambda : Var<X> Expr<Y> -> Expr<Fn<X,Y>>
c-style-switch : Expr<X: Eq> List<(Value<X> Expr<Y>)> -> Expr<Y>
cond : List<(Expr<Bool> Expr<Y>)> -> Expr<Y>
```

In a sense, this typechecking seems easy. We can use constructors rather than functions if we have GADTs.
