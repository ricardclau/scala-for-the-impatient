1. Create a gizmos hashmap and a second one with 10% of discounts

	```
	scala> val gizmos = Map("ps4" -> 400, "wiiu" -> 190, "3ds" -> 170, "x360" -> 450)
	gizmos: scala.collection.immutable.Map[String,Int] = Map(ps4 -> 400, wiiu -> 190, 3ds -> 170, x360 -> 450)

	scala> val discounts = for ((k,v) <- gizmos)  yield (k, v * (1 - 10f/100))
	discounts: scala.collection.immutable.Map[String,Float] = Map(ps4 -> 360.0, wiiu -> 171.0, 3ds -> 153.0, x360 -> 405.0)
	```

2. Program that reads words from a file

	```scala
	var words = collection.mutable.Map[String,Int]()
	val in = new java.util.Scanner(new java.io.File("fixtures/words-file.txt"))
	while (in.hasNext()) {
		val word = in.next
		val c = words.getOrElse(word, 0)
		words(word) = c + 1
	}
	words
	```

3. Same with an inmutable map

	```scala
	var words = Map[String,Int]()
	val in = new java.util.Scanner(new java.io.File("fixtures/words-file.txt"))
	while (in.hasNext()) {
		val word = in.next
		val c = words.getOrElse(word, 0)
		words += (word -> (c + 1))
	}
	words
	```

4. Same with a sorted map

	```scala
	var words = collection.immutable.SortedMap[String,Int]()
	val in = new java.util.Scanner(new java.io.File("fixtures/words-file.txt"))
	while (in.hasNext()) {
		val word = in.next
		val c = words.getOrElse(word, 0)
		words += (word -> (c + 1))
	}
	words
	```

5. Same with a java.util.TreeMap adapted

	```scala
	import collection.JavaConversions.mapAsScalaMap

	var words: collection.mutable.Map[String,Int] = new java.util.TreeMap[String, Int]
	val in = new java.util.Scanner(new java.io.File("fixtures/words-file.txt"))
	while (in.hasNext()) {
		val word = in.next
		val c = words.getOrElse(word, 0)
		words(word) = c + 1
	}
	words
	```

6. Linked hash map mapping days to Calendar

	```scala
	import java.util.Calendar._
	var days = collection.mutable.LinkedHashMap(
		"Monday" -> MONDAY,
		"Tuesday" -> TUESDAY,
		"Wednesday" -> WEDNESDAY,
		"Thursday" -> THURSDAY,
		"Friday" -> FRIDAY,
		"Saturday" -> SATURDAY,
		"Sunday" -> SUNDAY
	)

	for ((k, v) <- days) println(k + " -> " + v)
	```

7. Print a table of all java properties

	```scala
	import collection.JavaConversions.propertiesAsScalaMap
  	val props: collection.Map[String, String] = System.getProperties()
  	var maxLength = props.maxBy(_._1.length)._1.length
  	for ((k, v) <- props) {
  		println(k.padTo(maxLength, ' ') + " | " + v)
  	}
  	```

8. Function minmax(values: Array[Int])

	```scala
	def minmax(values: Array[Int]) = {
		(values.min, values.max)
	}
	```

9. Function lteqgt(values:Array[Int],v:int)

	```scala
	def lteqgt(values:Array[Int], v:Int) = {
		(
			(for (i <- values if i < v) yield i).length,
			(for (i <- values if i == v) yield i).length,
			(for (i <- values if i > v) yield i).length
		)
	}
	```

10. What happens when you zip together 2 strings???

	```
	scala> "Hello".zip("World")
	res13: scala.collection.immutable.IndexedSeq[(Char, Char)] = Vector((H,W), (e,o), (l,r), (l,l), (o,d))

	Use case? Diffing between strings?
	```
