# PHP-Design-Patterns
Singleton Pattern
Singleton pattern ensures that there will be only one instance, having a global access to it throughout the application.

Typical application of singleton pattern is creation of a database connection object, which must be created once in the lifetime of an application.

In the following code, the DataBaseConnector class can be instantiated only once, otherwise a message that disallows duplicate object will be issued.
