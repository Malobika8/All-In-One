# Intro

The *instanceof* operator in Java is not defined as a language construct that can be found in a particular class or package. Instead, it's a 
part of the Java language syntax and is used to test if an object is an instance of a particular class, an instance of a subclass, or an 
instance of a class that implements a particular interface.

## What is the instanceof Operator?

*instanceof* is a binary operator we use to test if an object is of a given type. The result of the operation is either true or false. It’s also known as a type comparison operator because it compares the instance with the type.

Before casting an unknown object, the instanceof check should always be used. Doing this helps to avoid a *ClassCastException* at runtime.

The instanceof operator’s basic syntax is:

```
(object) instanceof (type)
```

Now let’s see a basic example for the instanceof operator. First, we’ll create a class Round:

```
public class Round {
    // implementation details
}
```

Next, we’ll create a class Ring that extends Round:

```
public class Ring extends Round {
    // implementation details
}
```

We can use instanceof to check if an instance of Ring is of Round type:

```
@Test
void givenWhenInstanceIsCorrect_thenReturnTrue() {
    Ring ring = new Ring();
    assertTrue(ring instanceof Round);
}
```

## How Does the instanceof Operator Work?
The instanceof operator works on the principle of the is-a relationship. The concept of an is-a relationship is based on class inheritance 
or interface implementation.

# Read More

https://www.baeldung.com/java-instanceof
