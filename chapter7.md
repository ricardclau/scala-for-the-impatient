1. Write an example program to demonstrate that package com.horstmann.impatient is not the same as package com package horstmann package impatient

	```scala
	package com.horstmann {
	 object Test {
	    def apply() = println("Test")
	  }
	}

	package com.horstmann.impatient {
	  object Scope1 {
	    def apply(): Unit = {
	      // Test() will not work as com.horstmann has no visibility here
	      com.horstmann.Test()
	    }
	  }
	}

	package com {
	  package horstmann {
	    package impatient {
	      object Scope2 {
	        def apply(): Unit = {
	          Test()
	        }
	      }
	    }
	  }
	}
	```

2. Write a puzzler that baffles your Scala friends, using a package com that isn’t at the top level

	```scala
	// Not really sure what the author wants here...
	package chapter7.com

	class exercise2 {
	}
	```

3. Write a package random with functions nextInt(): Int, nextDouble(): Double, and setSeed(seed: Int): Unit. To generate random numbers, use the linear congruential generator next = previous × a + b mod 2n, where a = 1664525, b = 1013904223, and n = 32.

	```scala
	package object random {
		private var previous = 1
		private val a = 1664525
		private val b = 1013904223
		private val n = 32
		def nextInt(): Int = {
			previous = previous * a + b % (2 * n)
			previous
		}

		def nextDouble: Double = {
			nextInt
		}

		def setSeed(seed: Int) = { 
			previous = seed 
		}
	}

	package random { }
	```

4. Why do you think the Scala language designers provided the package object syntax instead of simply letting you add functions and variables to a package?

	```
	Since everything in Scala is an object, letting users adding functions and variables to a package violates this?
	```
	
5. What is the meaning of private[com] def giveRaise(rate: Double)? Is it useful?

	```
	It means the giveRaise method is visible up to the enclosing package com.
	But com is a very common top level package name so... not really useful here
	```	

6. Write a program that copies all elements from a Java hash map into a Scala
hash map. Use imports to rename both classes

	```scala
	import java.util.{HashMap => JavaMap}
	import scala.collection.mutable.{HashMap => ScalaMap}

	object CopyHashMaps extends App {
	  val a = new JavaMap[String, String]
	  a.put("a", "1")
	  a.put("b", "2")
	  a.put("c", "3")

	  val b = new ScalaMap[String, String]
	  val i = a.entrySet().iterator()
	  while (i.hasNext) {
	    val n = i.next()
	    b += ((n.getKey, n.getValue))
	  }
	}
	```	

7. Move the imports to the innermost scope

	```
	Imports can be anywhere so in this case they would be inside the object definition
	```	

8. What is the effect of import java._ import javax._ Is this a good idea?	

	```
	Everything under this 2 packages will be imported and collision problems can easily happen
	```

9. Write a program that imports the java.lang.System class, reads the user name from the user.name system property, reads a password from the Console object, and prints a message to the standard error stream if the password is not "secret". Otherwise, print a greeting to the standard output stream. Do not use any other imports, and do not use any qualified names (with dots)

	```scala
	import java.lang.System

	object Login extends App {
	  def apply() = {
	    val username = System getProperty("user.name")
	    val password = Console.readLine()

	    if (password equals "secret")
	      println("Welcome back" + username)
	    else
	      System.err.println("Invalid password")
	  }
	}
	```