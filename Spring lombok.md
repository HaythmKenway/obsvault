<iframe width="560" height="315" src="https://www.youtube.com/embed/videoseries?list=PL6oD2syjfW7CchnxJKhJ8IiY61efkyL8h" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

### Project Lumbok 
It is used to reduce the generation of boiler plate code this is done during compile time

@getter @setter is used make getters and setters

1. `@NoArgsConstructor`: This Lombok annotation generates a no-argument constructor for a class. A no-argument constructor is a constructor that takes no parameters. It initializes the object with default values or performs any necessary initialization. This annotation is useful when you want to create objects of a class without explicitly defining a constructor that takes arguments.

Here's an example:

```


`import lombok.NoArgsConstructor;
@NoArgsConstructor 
public class MyClass {     // Class members and methods }`
```

The above code, with the `@NoArgsConstructor` annotation, will automatically generate a no-argument constructor for the `MyClass` class.

2. `@AllArgsConstructor`: This Lombok annotation generates an all-argument constructor for a class. An all-argument constructor is a constructor that takes arguments corresponding to all the fields of a class. It initializes the object by assigning the provided values to the respective fields. This annotation is useful when you want to conveniently initialize all the fields of a class in a single constructor.

Here's an example:

```
import lombok.AllArgsConstructor;
@AllArgsConstructor
public class MyClass {
private int field1;
private String field2;
// Other class members and methods }
```


### Access Level 
we can apply access level for the classes as follows

```
@setter(AccessLevel.PRIVATE)
@GETTER(AccessLevel.PUBLIC)

```


### Tostring
