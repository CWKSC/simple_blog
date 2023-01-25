
# Don't use throw to replace null in parser combinator

Implementing the OOP version of Parser Combinator in C#.

Initially, I used null to represent parsing failure.

When I change to using throw exception and try-catch to handle it.

The performance **significantly** decreased.

Unworthy, don't do that.
