---
title: 'Classes and Objects: Inheritance'
currentMenu: csharp4python
---

## Inheritance

The notion of **inheritance** in C# is very similar as that in Python. One class may **extend** another class to inherit its fields and methods.

Recall that in Python the syntax for inheritance was the following:

```python
class Cat:
    # ...code for the Cat class...

class HouseCat(Cat):
    # ...code for the HouseCat class...
```

Any fields and non-constructor methods in `Cat` would be available to each instance of `HouseCat`. We express the inheritance relationship in plain English by saying the a `HouseCat` *extends* `Cat`.

In C#, the syntax for extending a class requires a colon (`:`) separating the two class names.

```csharp
public class Cat {
    // ...code for the Cat class...
}

public class HouseCat : Cat {
    // ...code for the HouseCat class...
}
```

We say that `HouseCat` is a **subclass** or **derived class** of `Cat`, and we say that `Cat` is the **base class** of `HouseCat`. In C#, a class may extend only one class.

As with Python, fields and non-constructor methods are directly available within the base class, and may be called as if the belonged to the based class, subject to any access modifiers. In general, this means that `private` and `internal` members of a base class are not accessible to a subclass. However, if the subclass and class are in the same assembly, `internal` would allow access to a member.

<aside class="aside-note" markdown="1">
This is a good time to review [access modifiers in C#](../introduction-to-classes-and-objects/#access-modifiers) if anything in the last paragraph was fuzzy.
</aside>

###

### Overriding Base Class Behavior

### The Object Class

#### Abstract Classes and Methods

## References

- [Inheritance in C# (msdn.microsoft.com)](https://msdn.microsoft.com/en-us/library/ms173149.aspx)
