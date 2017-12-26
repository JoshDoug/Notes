# GlassFish

The *current* JavaEE reference implementation, although it's being handed over to the Eclipse Foundation, so who knows what will happen.

* [Java EE Schemas](http://www.oracle.com/webfolder/technetwork/jsc/xml/ns/javaee/index.html)
* [Web Profile vs Full Platform - Stackoverflow](https://stackoverflow.com/questions/24239978/java-ee-web-profile-vs-java-ee-full-platform)
* [GlassFish Documentation](https://javaee.github.io/glassfish/documentation)

## GlassFish Commands

Prefix a command with the absolute or relative path to asadmin and then the subcommand to run, e.g. `/Applications/Servers/glassfish5/glassfish/bin/asadmin list-domains`, `glassfish/bin/asadmin list-domains`, or `./asadmin list-domains` to list the current domains and whether or not they're running.

`asadmin` subcommands:

* `list-domains` subcommand [documentation](https://docs.oracle.com/cd/E19798-01/821-1758/list-domains-1/index.html).
* `start-domain` subcommand, when domain is specified it defaults to `domain1`, to specify a domain: `start-domain domain2`
* `stop-domain domain1` - stop domain1.

## GlassFish 4

GlassFish 4.1.2 (and most likely any other version of GlassFish 4) can complain about the current version of Java being incorrect, e.g. "GlassFish requires Java SE version 6. Your JDK is version 0". On macOS, a workaround for this is to add `AS_JAVA=/Library/Java/JavaVirtualMachines/jdk1.8.0_152.jdk/Contents/Home` (or whatever the $JAVA_HOME for version 1.6-1.8 of Java is) to `glassfish4/glassfish/config/asenv.conf`.

Stackoverflow answer describing the solution (need to scroll down to the answer specifying macOS) [here](https://stackoverflow.com/questions/10444959/how-do-i-specify-the-jdk-for-a-glassfish-domain).