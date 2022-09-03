# Immutable Classes

## Learning Goals

- Explain immutable class
- Explain how this affects passing immutable types to methods

## Immutable Classes in Java

An **immutable class** is a class whose instances can never change values. For
example, the `String` class in Java is immutable, which means that once a
`String` object has a value, the value of that object cannot change.

This may seem counter-intuitive, since following Java code is valid:

```java
String aString = "initial value";
aString = "modified value";
```

This is because Java lets us change the value of an object of an immutable
type, but under the covers, it actually creates a new instance of that object
and assigns it to the new value for us. So the code in the previous example is
equivalent to the following:

```java
String aString = "initial value";
String anotherString = "modified value";
aString = anotherString;
```

The most common immutable types in Java are `String` and all the types that wrap
primitive types, such as `Boolean`, `Byte`, `Character`, `Integer`, `Long`,
`Float`, and `Double`.

## Pass Immutable Types to Methods

Wait, wait, wait... we just learned about pass-by-value and pass-by-reference.
Does this mean immutable types like `String` and `Integer` wouldn't work the
same way as the object `Example` worked in the past example?

Let's find out and replace our `int` variable type to an `Integer` value type:

```java
public class Example {
    public static void main(String[] args) {
        Integer number = 10;
        System.out.println("number before method call is " + number);
        change(number);
        System.out.println("number after method call is " + number);
    }

    public static void change(Integer numberCopy) {
        numberCopy = numberCopy + 2;
        System.out.println("numberCopy in the method call is " + numberCopy);
    }
}
```

When we run this code, we will get the following output:

```plainttext
number before method call is 10
numberCopy in the method call is 12
number after method call is 10
```

The value of number after the method call did not change! So what happened?

- When the code is first executed, we will enter the `main()` method and
  initialize `number` to the value of 10, just as we did before when the data
  type of `number` was an `int`.
- We output the value of `number` to the user to show that the value is 10.
- Then we will go into the `change()` method as we did before and pass
  `number`. This will pass it a copy of `number` and since an `Integer` is
  considered a reference, in memory, it points to an object in the heap - just
  as we saw when we passed an object before to a method! So when we copy the
  reference, we are copying the pointer too.

![Pass reference by value](https://curriculum-content.s3.amazonaws.com/java-mod-1/immutable-classes/Immutable-Object-1.png)

- The code now enters in the `change()` method and receives a copy of `number`.
  The receiving method chooses to call the copy of `number` `numberCopy`.
- At this point in time, `number` and `number` copy are both pointing to the
  same object in memory, so they have the same value of 10.
- When we reassign `numberCopy` to `numberCopy + 2`, what happens is something
  different from what we have seen before and that is because `Integer` is an
  immutable type. As we saw above with the `String` being reassigned, the same
  thing will happen here with the `Integer`. A new instance of `Integer` will
  be created, and then we will assign `numberCopy` that value instead. This is
  because an immutable object will not change state after it has been
  instantiated.

![Change Value](https://curriculum-content.s3.amazonaws.com/java-mod-1/immutable-classes/Immutable-Object-2.png)

- We will then print that the `numberCopy` has a value of 12 and exit the method
  `change()` since there are no more statements left to execute in the method.
- The code has now returned to the `main()` method and prints out the value of
  `number`, which is still 10 since the `numberCopy` parameter never modified
  the `Integer` instance that `number` references.
