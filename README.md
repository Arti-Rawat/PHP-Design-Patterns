# PHP-Design-Patterns
Singleton Pattern
Singleton pattern ensures that there will be only one instance, having a global access to it throughout the application.

Typical application of singleton pattern is creation of a database connection object, which must be created once in the lifetime of an application.

In the following code, the DataBaseConnector class can be instantiated only once, otherwise a message that disallows duplicate object will be issued.

[code]
<?php
   class DataBaseConnector {				
      private static $obj;				
      private final function __construct() {
         echo __CLASS__ . " object created for first time ". PHP_EOL;
      }
      public static function getConnect() {
         if (!isset(self::$obj)) {
            self::$obj = new DataBaseConnector();
            return self::$obj;
         } else {
            echo "connection object could not be created again" . PHP_EOL;
         }
      }
   }

   $obj1 = DataBaseConnector::getConnect();
   $obj2 = DataBaseConnector::getConnect();

   var_dump($obj1 == $obj2);
?>
DataBaseConnector object created for first time, 
connection object could not be created again,
bool(false)

Use Cases of Singleton Pattern
Database connections
Configuration settings
Logging
Caching mechanisms



Factory Pattern

In this pattern, you dont declare the object of the desired class directly, but another class is provided whose static method creates the required object.

The Factory Pattern is a creational design pattern that provides an interface for creating objects in a superclass but allows subclasses to alter the type of objects that will be created. It promotes loose coupling and helps manage object creation efficiently.



<?php
   class Automobile {
      private $bikeMake;
      private $bikeModel;

      public function __construct($make, $model) {
         $this->bikeMake = $make;
         $this->bikeModel = $model;
      }

      public function getMakeAndModel() {
         return $this->bikeMake . ' ' . $this->bikeModel;
      }
   }

   class AutomobileFactory {
      public static function create($make, $model) {
         return new Automobile($make, $model);
      }
   }

   $pulsar = AutomobileFactory::create('ktm', 'Pulsar');
   print_r($pulsar->getMakeAndModel());
?>

ktm Pulsar

Benefits of Factory Pattern
✔ Encapsulates Object Creation – Reduces dependencies on concrete classes.
✔ Loose Coupling – Client code depends only on the interface, not on the actual implementation.
✔ Easy to Extend – New notification types can be added without modifying the client code.



Strategy Pattern

The Strategy Pattern is a behavioral design pattern that enables selecting an algorithm at runtime. Instead of implementing multiple behaviors directly in a class, we define them as separate strategy classes and make the main class interchangeable with these strategies.

<?php
   interface example {
      public function case($str);
   }

   class ucase implements example {
      public function case($str) {
         return strtoupper($str);
      } 
   }

   class lcase implements example {
      public function case($str) {
         return strtolower($str);
      }
   }

   class testdata {
      private $data;

      public function __construct($input) {
         $this->data = $input;
      }
      public function process(example $type) {
         return $this->data = $type->case($this->data);
      }
   }
   $str = "hello";
   $obj = new testdata($str);
   echo $obj->process(new ucase) . PHP_EOL;  
   $str = "HELLO";
   echo $obj->process(new lcase);
?>

HELLO
Hello


Benefits of Strategy Pattern
✔ Encapsulates different algorithms – Each strategy is independent.
✔ Promotes Open/Closed Principle – New strategies can be added without modifying the existing code.
✔ Improves maintainability – Reduces complex if-else statements in business logic.

