# Install, Configuration, and General Usage of Web Servers
Covers notes on HTTP Servers, the related *AMP* stack, other stacks and integrating with related components.

## Apache HTTPD 2.4
### Combined with PHP
Useful doc mentioning/explaining PHP FPM/FastCGI, MPM Event, mod_rewrite/ProxyPass/ProxyPassMatch
* https://wiki.apache.org/httpd/PHP-FPM

PHP with Httpd:
Either as a module or via CGI?

mod_rewrite with PHP fpm/FastCGI issues:
* https://stackoverflow.com/questions/4117572/using-htaccess-with-fastcgi
* https://serverfault.com/questions/398834/understanding-apache-2-4-mod-proxy-fcgi-and-rewriterules-in-htaccess

Apache with PHP homebrew gist, lots of *no thanks* stuff in it, but useful to look over: https://gist.github.com/vitorbritto/4fea3514fa09ef298b1f

## Tomcat 8.5+ - [Tomcat Site](tomcat.apache.org)
