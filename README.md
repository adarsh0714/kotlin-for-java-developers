# kotlin-for-java-developers
https://www.coursera.org/learn/kotlin-for-java-developers

--- 
### Module 1
Learning Objectives
- List the key characteristics of Kotlin 
- Understand the types of tasks where Kotlin can be used 

### Module 2
Learning Objectives
- Convert Java code to Kotlin automatically
- Define variables and functions
  - `val` and `var`
  - 'val' denotes a read-only or assigned-once variable
  - 'var' denotes a mutable variable that can be modified
  - 'val' does not put any additional constraints on the stored object, and you can easily modify an object stored
    in 'val'. It doesn't say anything about the content that is stored.
  - it is recommended to declare new variables with 'val' to promote immutability and functional programming style.
  - In Kotlin, we have a distinction between mutable and read-only lists.
  - Understand when to specify function return types explicitly and when it is safe to omit them.
  - In Kotlin, you use the default arguments feature directly. You no longer need to provide several overloads.
- Use control structures
  - Kotlin does not have a ternary operator
  - "If" expression.
    ```
    val max = if (a > b) a else b
    ```
  - "When" expression.
    ```
    when (x) {
      1 -> print("x == 1")
      2 -> print("x == 2")
      else -> { // Note the block
        print("x is neither 1 nor 2")
      }
    }
    ```
    ```
    enum class Color {
      RED, ORANGE, YELLOW, GREEN, BLUE, INDIGO, VIOLET
    }
    fun getWarmth(color: Color) = when (color) {
      Color.RED, Color.ORANGE, Color.YELLOW -> "warm"
      Color.GREEN -> "neutral"
      Color.BLUE, Color.INDIGO, Color.VIOLET -> "cold"
    }
    ```
    ```
    val x = 1
    when {
      x.isOdd() -> print("x is odd")
      x.isEven() -> print("x is even")
      else -> print("x is funny")
    }
    ```
  - When expression is especially useful for more than two branches.
  - for, while, and do-while loops.
    ```
    for (item in collection) print(item)
    
    // iterating over range
    for (i in 1..3) { // including 3
      println(i)
    }
    
    for (i in 1 until 3) { // excluding 3
      println(i)
    }
    
    // iterating with a step
    for (i in 6 downTo 0 step 2) {
      println(i)
    }
    
    // element type
    val array = arrayOf("a", "b", "c")
    for (s: String in array) {
      println(s)
    }

    // iterating over a map
    for ((key, value) in map) {
      println("$key -> $value")
    }

    // iterating with index
    for ((index, value) in array.withIndex()) {
      println("the element at $index is $value")
    }
    ```
    ```
    while (x > 0) {
      x--
    }
    ```
    ```
    do {
      val y = retrieveData()
    } while (y != null) // y is visible here!
    ```
- Employ ranges
  - `in`
    - can be used to check if a value is in a range
    ```
    c in 'a'..'z'
    ```
    - can be used to iterate over a range
    ```
    for (i in 'a'..'z') { ... }
    ```
- Define and use extensions
  - Kotlin doesn't differentiate between checked and unchecked exceptions like Java.
  - `throw` is an expression in Kotlin
  - `try` is an expression in Kotlin
  - 
- Explain what is an extension function in Kotlin
  - Extension functions are utility functions that extend a class and can be called as regular member functions. They are defined outside of the class but can be easily discovered and used.
  ```
    fun String.lastChar() {
        return this.get(this.length - 1)
    }
  ```
  - The receiver of an extension function is the class that it extends, and it can be accessed using the "this" reference.
  - Extension functions need to be imported explicitly and are not accessible in the whole project by default.
  - from Java, it is treated as a regular static function.
  - If an extension has the same signature as a member function, the member function will always be chosen
  - Overloading members with extensions: It is possible to overload a member function with an extension by providing a different signature, such as different parameter types or a different number of parameters
  - Extensions cannot be overridden: Since extensions are resolved as static functions, they cannot be overridden in Kotlin.

### Module 3

Learning Objectives

- Distinguish nullable types and non-nullable types
  - Nullability refers to the ability of a variable to store null references.
  - Kotlin distinguishes between nullable types and non-nullable types. Non-nullable types can only store non-null objects, while nullable types can store both null and non-null values.
- Use different ways to perform an action only when a value of a nullable type is not null
  ```
  val s1: String = "always not null"
  val s2: String? = "can be null or not null"
  
  val length1 = s1.length // always safe
  val length2 = s2?.length // safe, will return null if s2 is null [safe access operator]
  val length2 = s2?.length ?: 0 // safe with default value, will return 0 if s2 is null [elvis operator]
  s2!!.length // unsafe, will throw NPE if s2 is null [non-null assertion operator]
  
  ```
  - It doesn't make sense to put two or more not-null assertion operators in one line. As you won't to be able to say which one cause the exception.
  - Under the hood, nullable types are implemented using annotations.
- Prefer safe operations for nullable values
- Employ functional programming style for manipulating collections
  - Lambdas are anonymous functions that can be used as expressions or passed as arguments to other functions.
  - filter, map, any, all, none, find, first/firstOrNull, count, partition, groupBy, associateBy, associate, zip, zipWithNext, flatten, flatMap
- Use function types
  - Kotlin allows you to store Lambdas in variables. The type of the variable in this case is called a function type
  - You can call variables of function type just like regular functions, providing all the necessary arguments.
  ```
  // example of function type
  val sum: (Int, Int) -> Int = { x: Int, y: Int -> x + y }
  ```
  - If you need to call a Lambda right in place, better user run.
  ```
  run { println("Hello") }
  ```
  - There is a difference between a function type that returns a nullable value and a nullable function type.
  ```
  val f: () -> Int? = { null } // function type that returns a nullable value
  val f: (() -> Int)? = null // nullable function type
  
  f?.invoke() // to call a nullable function type
  ```
- Member references
  - in Kotlin, you can store Lambda in a variable, however, you can't store a function in a variable.
  - You can store a reference to a function in a variable.
  ```
  fun isEven(i: Int): Boolean = i % 2 == 0
  
  val predicate: (Int) -> Boolean = ::isEven
  val predicate: (Int) -> Boolean = { it % 2 == 0 }
  
  // both are same
  ```
  - You can pass a function reference as an argument
  - There are two types of member references: bound and unbound references.
  - Bound references are created by specifying an object that the function is called on.
  - Unbound references are created by specifying the class that the function belongs to.
- Choose the right form of return expression for returning from lambda
  - In Kotlin, the return statement inside a lambda expression returns from the outer function, not just the lambda itself.
  - To return from a lambda, you can use a label.
  ```
    fun foo() {
      val ints = listOf(1, 2, 3, 4, 5)
      ints.forEach {
        if (it == 3) return // returns from foo
        print(it)
      }
      println("This point is unreachable")
    }
  
    fun foo() {
      val ints = listOf(1, 2, 3, 4, 5)
      ints.forEach lit@{
        if (it == 3) return@lit // returns from lambda expression
        print(it)
      }
      print(" done with explicit label")
    }
  ```

### Module 4

Learning Objectives

- Distinguish between different kinds of properties: without backing field, lazy, lateinit
- Summarize the differences in defining and using classes with Java
- Know the different syntax for constructors
- Use different kinds of classes for correct situations: enum, data, inner, sealed
- Use annotations to improve Java interoperability
- Explain the difference between object expression and object declaration
- Show the benefits of companion objects over static methods
- Give examples of using conventions in the standard library
- Employ conventions for your own classes

### Module 5

Learning Objectives

- Use short simple function from the standard library
- Explain why simple library functions bring no performance overhead
- Demonstrate how inlining works
- Describe the difference between operations on Collections and operations on Sequences
- Convert a chained call from Collections to Sequences
- Recognize lambdas with receiver in the code: in the standard library and different DSLs
- Illustrate in what sense lambdas with receiver are similar to extensions
- Show the Kotlin type hierarchy
- Explain the difference between Unit and Nothing types
- Recognize platform types: the types that came from Java
- Prevent NPEs for mixed Kotlin and Java code 
