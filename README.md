# Immutable Classes

## Learning Goals

- Explain immutable class

## Immutable Classes in Java

An immutable class is a class whose instances can never change values. For
example, the `String` class in Java is immutable, which means that once a
`String` object has a value, the value of that object cannot change.

This may seem counter-intuitive, since following Java code is valid:

```java
String aString = "initial value";
aString = "modified value";
```

This is because Java lets you change the value of an object of an immutable
type, but under the covers actually creates a new instance of that object and
assigns it to the new value for you. So that the code in the previous example is
equivalent to the following:

```java
String aString = "initial value";
String anotherString = "modified value";
aString = anotherString;
```

With the long-form code above, you should be able to see why the "value of
reference" mechanism does not work for objects of immutable types. It's because
every time an operation is applied to an object of immutable type, what Java
actually does is create a new reference and assign it to the previous variable.

The most common immutable types in Java are `String` and all the types that wrap
primitive types, such as `Integer`, `Boolean`, `Short`, ...

Even though Java doesn't let you directly access or manipulate the actual memory
location of an object, you can use the `identityHashCode` in the `System` class
to get a number that is an approximate representation of the memory address of a
specific object. This is not the exact location and may change without the
actual object reference changing in very specific cases. But it's good enough
for our purposes here, which are to observe how and when an object reference
changes.

Consider the following code:

```java
    public static void immutableString() {
        String sampleString = "initial value";
        System.out.println(sampleString);
        System.out.println("initial object \"address\" = " + System.identityHashCode(sampleString));
        sampleString = "modified value";
        System.out.println(sampleString);
        System.out.println("modified object \"address\" = " + System.identityHashCode(sampleString));
        }
```

Running this code will produce the following output:

```plaintext
initial value
initial object "address" = 245257410
modified value
modified object "address" = 1023892928
```

Of course, your values for the actual hashcode of the `String` object will be
different from the ones above, but you should still see that the address for the
initial and modified objects are different addresses.
