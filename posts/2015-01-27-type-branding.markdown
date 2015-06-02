---
title: Type Branding
author: Bob Long
---

Type branding is not a technique I have seen discussed much in the Haskell community, but I think
it's worth a look. It's easy to implement and gives us strong static assurances. I found an easy to
follow example from Oleg Kiselyov
[here](http://okmij.org/ftp/Haskell/eliminating-array-bound-check.lhs). He gives an example of
statically assuring array bounds using dependent types, then demonstrates similar safety using type
branding - which requires ExistentialQuantification and hidden constructors. The trick is to
introduce a type scope that's inescapable. Using this scoped type, "brand" the values on the type
level as being compatible and valid. This branding is the only place those data types are issued, so
we can just formally prove the section around the branding and use those types as
static verification.

I originally discovered branding through the [ad](https://github.com/ekmett/ad) library for [Automatic Differentiation](http://en.wikipedia.org/wiki/Automatic_differentiation). Here, it is used as a static assurance against confused infinitesimals in differential equations.
