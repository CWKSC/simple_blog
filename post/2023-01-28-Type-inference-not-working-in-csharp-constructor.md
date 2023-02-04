# Type inference not working in the C# constructor

```csharp
public class Foo<T> {
    public T value;
    public Foo(T value) {
        this.value = value;
    }
}
```

```csharp
var foo = new Foo(42); 
```

```
CS0305: Using the generic type 'generic type' requires 'number' type arguments
```

Type inference is not working in the C# constructor

You must add type arguments, like

```csharp
var foo = new Foo<int>(42); 
```

Straightforwardly, create a static function to solve this problem,

But somethings to care, the wrong way:

```csharp
public class Foo<T> {
    public T value;
    public Foo(T value) {
        this.value = value;
    }
    public static Foo<T> New<T>(T value) => new(value);
}
```

This not working because you need call like:

```csharp
var foo = Foo<int>.New(42);
```

The static function need to declare outside generic class

The correct way is:

```csharp
public class Foo<T> {
    public T value;
    public Foo(T value) {
        this.value = value;
    }
}
public class Foo {
    public static Foo<T> New<T>(T value) => new(value);
}
```

Then now we can,

```csharp
var foo = Foo.New(42);
```
