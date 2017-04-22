# Install, Configuration, and General Usage of Web Servers
Covers notes on HTTP Servers, the related *AMP* stack, other stacks and integrating with related components.

## Apache HTTPD 2.4

Useful doc mentioning/explaining PHP FPM/FastCGI, MPM Event, mod_rewrite/ProxyPass/ProxyPassMatch
* https://wiki.apache.org/httpd/PHP-FPM

PHP with Httpd:
Either as a module or via CGI?

Preworker, MPM Event, MPM Worker:
Confusing
* https://httpd.apache.org/docs/2.4/mpm.html
* https://serverfault.com/questions/231628/apache-mpms-worker-vs-prefork
* https://serverfault.com/questions/383526/how-do-i-select-which-apache-mpm-to-use
* http://www.binarytides.com/apache-mpm-php-server-api/
* https://www.liquidweb.com/kb/apache-mpms-explained/

mod_rewrite with PHP fpm/FastCGI issues:
* https://stackoverflow.com/questions/4117572/using-htaccess-with-fastcgi
* https://serverfault.com/questions/398834/understanding-apache-2-4-mod-proxy-fcgi-and-rewriterules-in-htaccess

Apache with PHP homebrew gist, lots of *no thanks* stuff in it, but useful to look over: https://gist.github.com/vitorbritto/4fea3514fa09ef298b1f

### Httpd Log
Located at: `/usr/local/var/log/apache2/error_log`

## Tomcat 8.5+ - [Tomcat Site](tomcat.apache.org)
