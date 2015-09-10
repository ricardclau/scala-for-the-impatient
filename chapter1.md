1. Methods applicable to 3. (using Tab in the REPL)

	```
	%   *   -   >    >>    ^              isInstanceOf   toChar     toFloat   toLong    toString   unary_-   |   
	&   +   /   >=   >>>   asInstanceOf   toByte         toDouble   toInt     toShort   unary_+    unary_~     
	```

2. Float numbers precision

	```
	scala> sqrt(3)
	res35: Double = 1.7320508075688772

	scala> pow(res35, 2)
	res36: Double = 2.9999999999999996
	```

3. res variables are val

4. \* operator repeats the string N times.

	```
	scala> "crazy" * 3
	res37: String = crazycrazycrazy
	```

	In ScalaDoc, inside StringOps http://www.scala-lang.org/api/current/#scala.collection.immutable.StringOps

5. It would be another way of doing 10.pow(2) where 2 is inferred. The operation fails as the pow method exists in the BigInt class (not in RichInt)

	```
	scala> 10 pow 2
	<console>:17: error: value pow is not a member of Int
	       10 pow 2
	          ^

	scala> BigInt(10) pow 2
	res43: scala.math.BigInt = 100
	```

6. We need to use BigInt so...

	```
	scala> BigInt(2) pow 1024
	res44: scala.math.BigInt = 179769313486231590772930519078902473361797697894230657273430081157732675805500963132708477322407536021120113879871393357658789768814416622492847430639474124377767893424865485276302219601246094119453082952085005768838150682342462881473913110540827237163350510684586298239947245938479716304835356329624224137216
	```

7. probablePrime(100, Random) needs to import BigInt._ and util._

	```
	scala> import BigInt._
	import BigInt._

	scala> import util._
	import util._

	scala> probablePrime(100, Random)
	res47: scala.math.BigInt = 1201461450774509927910049336247
	```

8. Convert a number to base36

	```
	scala> abs(util.Random.nextInt).toString(36)
	res52: String = csbxqa
	```

9. First and last character for a String

	```
	scala> "abcde"(0)
	res60: Char = a

	scala> "abcde".last
	res61: Char = e
	```

10. Better semantics over substring?

	```
	scala> "abcde".take(2)
	res62: String = ab

	scala> "abcde".drop(2)
	res63: String = cde

	scala> "abcde".takeRight(2)
	res64: String = de

	scala> "abcde".dropRight(2)
	res65: String = abc
	```