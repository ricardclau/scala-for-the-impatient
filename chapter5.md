1. Improve the Counter class so that it does not turn negative at Int.MaxValue

	```scala
	class Counter {
		private var value = 0
		def increment() { if (value < Int.MaxValue) value += 1 }
		def current = value
	}
	```

2. BankAccount with deposit and withdraw and a read-only property balance

	```scala
	class BankAccount {
		private val _balance: Double = 0.0
		def deposit(money: Double)  { _balance += money }
		def withdraw(money: Double) {
			if (money > _balance) {
				throw new Exception("Not enough money")
			}
			_balance -= money
		}
		def balance = _balance
	}
	```

3. Class Time with read-only properties hours and minutes and a method before(other: Time): Boolean. Constructor like new Time(hrs, min)

	```scala
	class Time(val hrs: Int, val min: Int) {
		if (hrs < 0 || hrs > 23) {
			throw new Exception("Invalid hour")
		}

		if (min < 0 || min > 59) {
			throw new Exception("Invalid min")
		}

		def before(other: Time) : Boolean = {
			(hrs < other.hrs || hrs == other.hrs && min < other.min)
		}
	}
	```

4. Same class signature but internal representations as an integer

	```scala
	class Time(hrs: Int, min: Int) {
		if (hrs < 0 || hrs > 23) {
			throw new Exception("Invalid hour")
		}

		if (min < 0 || min > 59) {
			throw new Exception("Invalid min")
		}

		private val _time = hrs * 60 + min

		def before(other: Time) : Boolean = {
			_time < other._time
		}
	}
	```

5. Class Student with read-write JavaBeans properties name (String) and id (Long).

	```scala
	import beans.BeanProperty
	class Student() {
		@BeanProperty var name: String = _
		@BeanProperty var id: Long = _
	}
	```

	```
	scala> val a = new Student
	a: Student = Student@5dbae6f7

	scala> a.
	asInstanceOf   getId   getName   id   id_=   isInstanceOf   name   name_=   setId   setName   toString

	You can call setXXX and getXXX but apparently this is verbose and less intuitive in Scala world...
	```

6. Primary constructor that turns negative ages to 0

	```scala
	class Person(var name: String, var age: Int) {
		if (age < 0) age = 0
	}
	```

7. Person accepting String with first name, space and last name

	```scala
	class Person(val fullName: String) {
		val firstName = fullName.split(' ')(0)
		val lastName = fullName.split(' ')(1)
	}
	```

8. Make a class Car with with read-only properties for manufacturer, model name, and model year, and a read-write property for the license plate. Supply four constructors. All require the manufacturer and model name. Optionally, model year and license plate can also be specified in the constructor. If not, the model year is set to -1 and the license plate to the empty string. Which constructor are you choosing as the primary constructor? Why?

	```scala
	class Car(val manufacturer: String, val model: String, val year: Integer = -1, var plate: String = "") {
		def this(manufacturer: String, model: String, plate: String) = {
			this(manufacturer, model, -1, plate)
		}

		override def toString = "[" + manufacturer + ", " + model + ", " + year + ", '" + plate + "']"
	}
	```

	```
	I am choosing the constructor with most # of parameters as the primary one since it is always easy to call it from the other constructors with less parameters just sending the default values.
	```

9. Reimplement this class in Java

	```java
	public class Car {
		private String manufacturer;
		private String model;
		private int year = -1;
		private String plate = "";

		public Car(String manufacturer, String model, int year, String plate) {
			this.manufacturer = manufacturer;
			this.model = model;
			this.year = year;
			this.plate = plate;
		}

		public Car(String manufacturer, String model, String plate) {
			this.manufacturer = manufacturer;
			this.model = model;
			this.plate = plate;
		}

		public Car(String manufacturer, String model, int year) {
			this.manufacturer = manufacturer;
			this.model = model;
			this.year = year;
		}

		public Car(String manufacturer, String model) {
			this.manufacturer = manufacturer;
			this.model = model;
		}

		public String getManufacturer() {
			return manufacturer;
		}

		public String getModel() {
			return model;
		}

		public int getYear() {
			return year;
		}

		public String getPlate() {
			return plate;
		}

		public void setPlate(String plate) {
			this.plate = plate;
		}
	}

	```

10. Consider a class and rewrite it to use explicit fields

	```scala
	class Employee(val name: String, var salary: Double) {
		def this() { this("John Q. Public", 0.0) }
	}
	```

	```scala
	class Employee {
		private var _name = "John Q. Public"
		var salary = 0.0

		def this(n: String, s: Double) {
			this()
			_name = n
			salary = s
		}

		def name = _name
	}
	```


