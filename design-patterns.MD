# Design pattern revision


## Factory method


* Type: `creational design pattern`

* In Factory pattern, we create object without exposing the creation logic to client and the client use the same common interface to create new type of object.
* The idea is to use a static member-function (static factory method) which creates & returns instances, hiding the details of class modules from user.

Example:
> Say, in a ‘Drawing’ system, depending on user’s input, different pictures like square, rectangle, circle can be drawn. Here we can use factory method to create instances depending on user’s input. For adding new type of shape, no need to change client’s code.


## Observer Pattern

> Publishers + Subcribers = Oserver Pattern

* When to use: You should consider using this pattern in your application when multiple objects are dependent on the state of one object as it provides a neat and well tested design for the same.

* Example: Social media, RSS feeds, email subscription in which you have the option to follow or subscribe and you receive latest notification.


## Singleton 

> The singleton pattern is a design pattern that restricts the instantiation of a class to one object. 

### Method 1: Classic Implementation 
```Java
// Classical Java implementation of singleton
// design pattern
class Singleton
{
    private static Singleton obj;
 
    // private constructor to force use of
    // getInstance() to create Singleton object
    private Singleton() {}
 
    public static Singleton getInstance()
    {
        if (obj==null)
            obj = new Singleton();
        return obj;
    }
}
```
*Note: Not safe for multithread*


### Method 2: make getInstance() synchronized 

```Java
// Thread Synchronized Java implementation of
// singleton design pattern
class Singleton
{
    private static Singleton obj;
 
    private Singleton() {}
 
    // Only one thread can execute this at a time
    public static synchronized Singleton getInstance()
    {
        if (obj==null)
            obj = new Singleton();
        return obj;
    }
}
```
*Note: Solve the problem of method 1, but decrease the perfomance*


### Method 3: Eager Instantiation 

```Java
// Static initializer based Java implementation of
// singleton design pattern
class Singleton
{
    private static Singleton obj = new Singleton();
 
    private Singleton() {}
 
    public static Singleton getInstance()
    {
        return obj;
    }
}
```

### Method 4 (Best): Use “Double Checked Locking” 

```java

// Double Checked Locking based Java implementation of
// singleton design pattern
class Singleton
{
    private static volatile Singleton obj  = null;
 
    private Singleton() {}
 
    public static Singleton getInstance()
    {
        if (obj == null)
        {
            // To make thread safe
            synchronized (Singleton.class)
            {
                // check again as multiple threads
                // can reach above step
                if (obj==null)
                    obj = new Singleton();
            }
        }
        return obj;
    }
}
```

*Note: This method drastically reduces the overhead of calling the synchronized method every time.*

> Example: Hardware interface access: The use of singleton depends on the requirements. Singleton classes are also used to prevent concurrent access of class. Practically singleton can be used in case external hardware resource usage limitation required e.g. Hardware printers where the print spooler can be made a singleton to avoid multiple concurrent accesses and creating deadlock.


