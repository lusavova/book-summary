# Too Many Parameters in Java Methods

Having too many method parameters affects the code readability and can cause lots of possible bugs. These bugs are hard to find.
There are some things we can do to avoid using multiple constructor or method parameters.

1. Using custom types:

    These custom types might be implemented as Data Transfer Objects (DTOs), JavaBeans, Value Objects, Reference Objects or any other custom type (typically a class or enum).

    Example:
    ```java
        public Person createPerson( 
            String lastName,
            String firstName,
            String middleName,
            String streetAddress,
            String city,
            String state,
            boolean isFemale,
            boolean isEmployed) {
        // ...
    }
    ```
    In this example we can accidentally pass parameters in the wrong order. Some improvement can be made by varying the types in the parameter list.

    Improvement:
    ```java
        public Person createPerson( 
            Name firstName,
            Name middleName,
            Name lastName,
            Address streetAddress,
            City city,
            State state,
            Enum gender,
            EmploymentStatus employment) {
        // ...
    }
    ```

    The three names are still a potential issue as the caller could provide them out of order, but we could write specific classes for FirstName, LastName, and MiddleName or create new class that represents a full name and has all three of those names as its attributes.

    ADVANTAGES:

    Having multiple parameters of the same type makes it easier for the developer to mix up the order. It also reduces the ability of the IDE to match the appropriate suggestion with the parameter when using code completion. These custom types are helpful to an IDE as static compile-time checking. In general, it is better to move as much automatic checking as possible from runtime to compile time. The existence of these custom types makes it more flexible, because it's easier to add more details in the future.

    DISADVANTAGES:

    The custom type approach adds overhead of extra instantiations and use of memory. For example, the Name class requires instantiation of the Name class itself AND its encapsulated String. Also adds extra effort to write and test these custom types.