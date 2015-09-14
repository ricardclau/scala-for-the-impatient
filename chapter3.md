1. Create an array of N random integers

	```scala
	def RandomInts(n: Int) = {
		val a = new Array[Int](n)
		for (i <- 0 until a.length) {
			a(i) = util.Random.nextInt
		}
		a
	}

	var a = RandomInts(6)
	```

2. Loop that swaps adjacent elements

	```scala
	def swap(a: Array[Int]) = {
		for (i <- 0 until (if (a.length % 2 == 0) a.length else a.length - 1, 2)) {
			val tmp = a(i)
			a(i) = a(i+1)
			a(i+1) = tmp
		}
		a
	}
	```

	```
	scala> swap(Array(1,2,3,4,5))
	res34: Array[Int] = Array(2, 1, 4, 3, 5)

	scala> swap(Array(1,2,3,4,5,6))
	res35: Array[Int] = Array(2, 1, 4, 3, 6, 5)

	scala> swap(Array(1))
	res36: Array[Int] = Array(1)

	scala> swap(Array())
	res37: Array[Int] = Array()
	```

3. Same but using for / yield

	```scala
	for (i <- 0 until a.length) yield if (a.length % 2 == 1 && a(i) == a.last) a(i) else if (i % 2 == 0) a(i+1) else a(i-1)
	```

4. First positives, then zeroes, then negatives!!!

	```scala
	def PosZeroNeg(a: Array[Int]) = {
		val b = new ArrayBuffer[Int]
		b ++= (for (i <- a if i > 0) yield i)
		b ++= (for (i <- a if i == 0) yield i)
		b ++= (for (i <- a if i < 0) yield i)
		b
	}

	PosZeroNeg(Array(2,6,-1,9,0,-4,-6))
	```

5. Compute the avg of an integers array

	```
	scala> var a = Array(1,2,3,4,7,12)
	a: Array[Int] = Array(1, 2, 3, 4, 7, 12)

	/** Is there a better way to ensure a Double??? */
	scala> (a.sum * 1.0) / a.length
	res56: Double = 4.833333333333333	
	```

6. Reverse sort for Array and ArrayBuffer

	```
	/** Using a quicksort in place */
	scala> var a = Array(1,2,4,5,3)
	a: Array[Int] = Array(1, 2, 4, 5, 3)

	scala> util.Sorting.quickSort(a)

	scala> a.reverse
	res62: Array[Int] = Array(5, 4, 3, 2, 1)

	/** This is not in place but works */
	scala> var a = Array(1,2,4,5,3)
	a: Array[Int] = Array(1, 2, 4, 5, 3)

	scala> a.sortWith(_.compareTo(_) > 0)
	res58: Array[Int] = Array(5, 4, 3, 2, 1)

	/* In ArrayBuffers ... quickSort in place fails */
	scala> var a = ArrayBuffer(1,2,4,5,3)
	a: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(1, 2, 4, 5, 3)

	scala> util.Sorting.quickSort(a)
	<console>:13: error: overloaded method value quickSort with alternatives:
	  [K](a: Array[K])(implicit evidence$1: scala.math.Ordering[K])Unit <and>
	  (a: Array[Float])Unit <and>
	  (a: Array[Int])Unit <and>
	  (a: Array[Double])Unit
	 cannot be applied to (scala.collection.mutable.ArrayBuffer[Int])
	       util.Sorting.quickSort(a)

	/** But the sortWith lambda works */
	scala> var a = ArrayBuffer(1,2,4,5,3)
	a: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(1, 2, 4, 5, 3)

	scala> a.sortWith(_.compareTo(_) > 0)
	res64: scala.collection.mutable.ArrayBuffer[Int] = ArrayBuffer(5, 4, 3, 2, 1)
	```

7. Code snippet to remove duplicates

	```
	scala> Array(1,2,4,5,4,5,2).distinct
	res65: Array[Int] = Array(1, 2, 4, 5)
	```

8. Use drop changing the snippet

	```scala
	a = ArrayBuffer[Int](2, 6, -1, 9, 0, -4, 6, -1, 8)

	var indexes = for (i <- 0 until a.size if a(i) < 0) yield i
	indexes = indexes.drop(1)
	for (j <- indexes.reverse) a.remove(j)
	```	

9. Sort all timezones in America

	```scala
	java.util.TimeZone.getAvailableIDs().filter(_.startsWith("America") ).map(_.drop("America/".length)).sortWith(_ < _)
	```

10. Java / Scala interoperability

	```scala
	import java.awt.datatransfer._	
	val flavors = SystemFlavorMap.getDefaultFlavorMap().asInstanceOf[SystemFlavorMap]	
	collection.JavaConversions.asScalaBuffer(flavors.getNativesForFlavor(DataFlavor.imageFlavor))
	```

	```
	scala> collection.JavaConversions.asScalaBuffer(flavors.getNativesForFlavor(DataFlavor.imageFlavor))
	res1: scala.collection.mutable.Buffer[String] = Buffer(PNG, JFIF, TIFF)

	scala> flavors.getNativesForFlavor(DataFlavor.imageFlavor)
	res2: java.util.List[String] = [PNG, JFIF, TIFF]
	```
