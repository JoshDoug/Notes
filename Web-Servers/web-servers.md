# Install, Configuration, and General Usage of Web Servers

Covers notes on HTTP Servers, the related *AMP* stack, other stacks and integrating with related components.
Notes should be scoped to mention of and a quick summary of a server and relevant versions, links to sites and documentation, and info on integrating with other relevant components. If the explanation gets beyond a certain point it should be moved into its own file.

* [Digital Ocean blog post - Apache vs Nginx](https://www.digitalocean.com/community/tutorials/apache-vs-nginx-practical-considerations)

## Apache HTTPD 2.4

### Combined with PHP

Useful doc mentioning/explaining PHP FPM/FastCGI, MPM Event, mod_rewrite/ProxyPass/ProxyPassMatch

* [Apache httpd wiki on PHP-FPM](https://wiki.apache.org/httpd/PHP-FPM)

PHP with Httpd:
Either as a module or via CGI?

mod_rewrite with PHP fpm/FastCGI issues:

* [Using htaccess with fastcgi](https://stackoverflow.com/questions/4117572/using-htaccess-with-fastcgi)
* [Understanding Apache mod proxy fcgi and rewrite rules in htaccess](https://serverfault.com/questions/398834/understanding-apache-2-4-mod-proxy-fcgi-and-rewriterules-in-htaccess)

Apache with PHP homebrew gist, lots of *no thanks* stuff in it, but useful to look over, [gist here](https://gist.github.com/vitorbritto/4fea3514fa09ef298b1f)

## [Nginx](https://nginx.org/)

## [lighttpd](https://www.lighttpd.net/)

Designed to be lightweight.

## [Caddy](https://caddyserver.com/)

Written in Go, free and open source with pricing options for Enterprise and sponsorship.

## [IIS](https://www.iis.net/)

## Java Focused Servers

Java Servers are covered in Java > Servers.

## [Apache Tomcat](tomcat.apache.org)

* Current Stable Version of Tomcat: 8.5.+
* Older Stable: 8.0.+
* Preview version: 9.+

As Tomcat is java based there isn't a lengthy install, just unzip the binary in a directory and configure it, either in an IDE or with the OS.

## [Apache TomEE](https://tomee.apache.org/)

## [Jetty](https://www.eclipse.org/jetty/)

An Eclipse Project.

## [GlassFish](https://glassfish.java.net/)