# Log4j 2 info
This might make sense to move into its own folder at some point if I note down info on any other Java based logging utils.

configuration info: (docs are not great/beginner friendly with log4j)
https://logging.apache.org/log4j/2.x/manual/configuration.html

Configuration of Log4j 2 can be accomplished in 1 of 4 ways:

1. Through a configuration file written in XML, JSON, YAML, or properties format.
2. Programmatically, by creating a ConfigurationFactory and Configuration implementation.
3. Programmatically, by calling the APIs exposed in the Configuration interface to add components to the default configuration.
4. Programmatically, by calling methods on the internal Logger class.

Programmatic configuration:
* Extending Log4j 2: https://logging.apache.org/log4j/2.x/manual/extending.html
* Programmatic Log4j Configuration: https://logging.apache.org/log4j/2.x/manual/customconfig.html

# SLF4J
These notes should probably also cover SLF4J - The Simple Logging Facade for Java, as this can be used with log4j to avoid lock in, but also seems to cause issues right off the bat if you don't know how to configure log4j properly (and how the h*ck do you do that).
