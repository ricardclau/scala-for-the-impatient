1. Write an object Conversions with methods inchesToCentimeters, gallonsToLiters, milesToKilometers

	```scala
	object Conversions {
		def inchesToCentimeters(in: Double) = 2.54 * in
		def gallonsToLiters(in: Double) = 3.78541178 * in
		def milesToKilometers(in: Double) = 1.609344 * in
	}
	```

2. Make it more object oriented with a superclass and 3 objects

	```scala
	class UnitConversion(val factor: Double) {
		def apply(in: Double) = in * factor
		def convert(in: Double) = in * factor
	}

	object inchesToCentimeters extends UnitConversion(2.54) {}
	object gallonsToLiters extends UnitConversion(3.78541178) {}
	object milesToKilometers extends UnitConversion(1.609344) {}
	```

3. Define an object Origin that extends from java.awt.Point. Why is this not a good idea?

	```scala
	object Origin extends java.awt.Point {}
	```

	```
	scala> val a = Origin
	a: Origin.type = Origin$[x=0,y=0]

	scala> a.
	asInstanceOf   distance     getLocation   getY           move          toString    x
	clone          distanceSq   getX          isInstanceOf   setLocation   translate   y

	It is not a good idea because methods like move or setLocation are not great for an Origin???
	```

4. Define a Point with a companion object with apply

	```scala
	class Point(val x: Double, val y: Double) {}

	object Point {
		def apply(x: Double, y: Double) = new Point(x, y)
	}
	```

5. Scala Application printing the command-line arguments in reverse order

	```scala
	class Reverse extends App {
		println(args.reverse.mkString(" "))
	}
	```

6. Write an enumeration describing the four playing card suits so that the toString method returns the nice unicode character

	```scala
	object PokerSuits extends Enumeration {
		val Hearts = Value("♥")
		val Diamonds = Value("♦")
		val Clubs = Value("♣")
		val Spades = Value("♠")
	}

	println(PokerSuits.values)
	```

7. Write a function that checks if a card suit is red

	```scala
	object PokerSuits extends Enumeration {
		type PokerSuits = Value
		val Hearts = Value("♥")
		val Diamonds = Value("♦")
		val Clubs = Value("♣")
		val Spades = Value("♠")

		def isRed(p: PokerSuits): Boolean = { return p == Hearts || p == Diamonds }
	}

	println(for (s <- PokerSuits.values) yield (s, PokerSuits.isRed(s)))
	```

8. Write an enumeration for the eight corners of the RGB color cube

	```scala
	object RGBCube extends Enumeration {
		type RGBCube = Value
		val black = Value(0x000000, "Black")
		val red = Value(0xff0000, "Red")
		val green = Value(0x00ff00, "Green")
		val blue = Value(0x0000ff, "Blue")
		val yellow = Value(0xffff00, "Yellow")
		val magenta = Value(0xff00ff, "Magenta")
		val cyan = Value(0x00ffff, "Cyan")
		val white = Value(0xffffff, "White")
	}

	for(c <- RGBCube.values ) println("0x%06x: %s".format(c.id, c))
	```
