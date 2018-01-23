# Item 1: Static factory method (SFM) instead constructor

## Pros:
- SFM has name
- not require to create new object each time
- can return object of any subtype of return type
- returned class can be different as function of input parameters
- returned class need not exists when SFM is written (service provider frameworks)

## Cons:
- class without public or protected constuctor can not be subclassed
- hard for programmers to find


# Item 2: Builder for many constructor parameters

- telescoping constructor pattern works but it's hard to write client code for many parameters and is't harder to read it
- second alternative is JavaBean pattern
- simulates named optional parameters

# Pros
- well suited to class hierarchies
- multiple varargs
- can aggregate parrameters passed into multiple calls of method

# Cons
- another object creation (Builder)
- more verbose than telescopiing constructor
- harder to switch to builder later when num of params increase


# Item 3: Enforce singleton with private constructor or enum type

- making class singleton can make it difficult to test its clients

## Member final field Singleton
- privileged client can invoke constructor reflectively (modify constructor to throw exception when second instance is created

## Member factory method Singleton (e.g. getInstance())
- same problem as above
- makes API clear that this is singleton
- can be changed in future to non singleton without API change
- generic singleton factory can be wrote
- method reference can be used as Supplier

When none of advantaged is relevant first approach is preferable.

To make this singleton serializable it isn't sufficient to implement Serializable => declare all fields transient and provide readResolve() method

## Single element enum Singleton
- serialization for free
- not suffering reflection attack
- cannot be used if singleton need extend superclass


# Item 4: Enforce noninstability with a private constructor

- for utility class
- methods can be added to interface
- group methods on final class
- private constructor with throws exception => non instantability (exception is not required)
- class without public or protected constructor can not be subclassed


# Item 5: Prefer dependency injection to hardwiring resources

- static utility clases and singletons are inpropriate for classes with dependencies or underlying resources
- pass resource to constructor when creating new instance
- paas resource factory to constructor (Supplier<T> interface>

## Pros
- imporves readablility and testability

## Cons
- can clutter up big projects (dependency injection framework can help)


# Item 6: Avoid creating unnecessary objects

- object can be allways reused if it's immutable
- constructor must create new object each time it's called
- prefer primitives to boxed primitives
- watch out for unintentional autoboxing
- object pool for non heavyweight object is bad idea


# Item 7: Eliminate obsolete object references

- think about memory management 
- represent cache as WeakMap
- memory leak in listeners and callbacks


# Item 8: Avoid finalizers and cleaners

- finalizers are unpredictable, often dangerous and generaly unnecessary
- cleaners are Java 9 replacment for finalizers
- never do anything time critical in finalizers or cleaners
- performance penality for using
- finalizers are security problem => final classes are immune, for non final override empty finalizer and make it final
- good as safety net


# Item 9: Prefer try-with-resources to try-finally

- try-finally is ugly with more than one resource
