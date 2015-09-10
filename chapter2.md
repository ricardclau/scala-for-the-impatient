1. Function signum

	```scala
	def signum(n: Int) : Int = {
		if (n > 0) 1
		else if (n < 0) -1
		else 0
	}
	```

2. Type Unit value ()

3. Very weird and misleading but... 

	```
	scala> var y = 0
	y: Int = 0

	scala> var x: Unit = y = 1
	x: Unit = ()

	scala> x = y = 1
	x: Unit = ()
	```

4. We need to specify the second argument for the to method

	```
	scala> for (i <- 10 to (0, -1)) { println(i) }
	```

	or... with named arguments

	```
	scala> for (i <- 10 to (end = 0, step = -1)) { println(i) }
	```

5. Procedure for a countdown function

	```scala
	def countdown(n: Int) {
		for (i <- n to (0, -1)) println(i)
	}
	```

6. For loop to multiply the unicode characters

	```
	scala> var total = 1L
	total: Long = 1

	scala> for (c <- "Hello") total *= c

	scala> total
	res22: Int = 9415087488
	```

7. Scala obscurity!

	```
	scala> "Hello".foldLeft(1L)((a,b) => a*b)
	res23: Int = 9415087488
	```

8. Write a function for product

	```scala
	def product(word: String) = {
		word.foldLeft(1L)((a,b) => a*b)
	}
	```

9. Recursive way

	```scala
	def productRec(word: String) : Long = {
		if (word.isEmpty) 1L		
		else word(0) * productRec(word.drop(1))
	}
	```

10. Recursive pow

	```scala
	def xton(x: Double, n: Int): Double = {
		if (n == 0) 1
		else if (n < 0) 1 / xton(x, -n)
		else if (n % 2 == 0) xton(x, n/2) * xton(x, n/2)
		else x * xton(x, n - 1)	
	}
	```
