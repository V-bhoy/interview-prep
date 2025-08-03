## Classes

- it is a blueprint, a logical entity which defines some properties and behaviour.
- it is declared only once
- defined with keyword 'class'
- a file can have multiple classes, but it can have only one public class which is same as the name of the file.
- This is done to avoid ambiguity and make it easier for the compiler to locate the primary class with the main method and associate it with the file.
- When a class is defined, no memory is allocated to the class in heap and stack memory.
- Although its metadata information is stored in metaspace, when the class is first loaded into memory.
### What is meta space?
-	In Java 8 and later, class metadata is stored in Metaspace, which is a memory area in native (non-heap) memory.
- Before Java 8, it was stored in a space called PermGen, which had a fixed size. Metaspace grows dynamically (unless limited).
### When is the class loaded?
- A class is loaded into memory (and its metadata into Metaspace) only when it is first needed at runtime. This is handled by the ClassLoader.
``` java
public class Main {
   public static void main(String[] args) {
      Dog d = new Dog();  // Dog class is loaded here
   }
}
```
- Main class is loaded first.
- When the Dog object is created, JVM loads Dog.class and stores its metadata into Metaspace.
### To note:
- When you stop your application or the file is executed, the entire memory (including Metaspace) is cleared.
- So, if you run the application again, JVM loads all required classes again and stores their metadata into a fresh Metaspace area.
### Does Metaspace affect JVM performance?
- Yes, if too many classes are loaded dynamically (e.g., in frameworks like Spring), Metaspace can grow large and lead to OutOfMemoryError if not managed.

```java
 class Dog {
    String name;
    int age;
    String colour;
    String breed;
    // behaviour
    void walk(){
      System.out.println(this.name+" walks.");
    }
    void bark(){
       System.out.println(this.name+" barks.");
    }
}
```

## Objects
- it is a physical entity
- it is an instance of a class which has all the predefined properties and behaviour defined in the class attached with it
- When an object is created, memory is allocated to it in the heap memory.
- We can create multiple objects from a class
- objects are created using new keyword followed by calling the constructor of the class
```java
   Dog dog = new Dog();
   // you can access all the properties and methods for the class through dog object.
   dog.name = "Tom";
   dog.age = 2
   dog.colour = "white";
   dog.breed = "Labrador";
   dog.walk();
   dog.bark();
```
