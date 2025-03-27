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
