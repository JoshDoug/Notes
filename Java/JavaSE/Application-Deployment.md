# Deploying Java Applications
https://docs.oracle.com/javase/tutorial/deployment/index.html

https://docs.oracle.com/javase/8/docs/technotes/guides/deploy/toc.html

Covers:
* Deploying Web Start Applications (neat)
* Java Rich Internet Applications ?
* Deployment In-Depth
* Deploying Self-Container Applications
* Packaging Programs in JAR Files

The Oracle tutorial also covers deploying Applets, but they're no longer relevant so why bother reading up on it.

## Java Web Start Applications
Java Web Start (JWS) allows fully featured apps to be downloaded and run with a single click (after multiple security prompts have been clicked through...), but there is no installation process, just click a link on a web page, which points to a Java Network Launch Protocol (JNLP) file that communicates with the Java Web Start software to download, cache, and run the app.

Apparently updates to a JWS app are automatically downloaded when the application is run standalone from a user's desktop?

Not sure why they try to make it sound all fancy, because a JWS is in essence an XML or 'JNLP' File that the JRE will recognise, that refers to the location of the jar via a link, which then downloads the jar and runs it.

So for someone that wants to use it, it's as simple as: make a jar for your app and host it on a server, create an xml file that describes it with the appropiate elements, create an HTML page that links to the XML/JNLP file. Easy.

The HTML File, JNLP File, and Jar/App don't have to exist on the same server.

Links:
* https://docs.oracle.com/javase/tutorial/deployment/webstart/index.html
* https://docs.oracle.com/javase/8/docs/technotes/guides/javaws/developersguide/contents.html
* https://docs.oracle.com/javase/8/docs/technotes/guides/javaws/

### Developing a Java Web Start Application
Running into a security issue for some reason.

#### Setting up the JNLP File
https://docs.oracle.com/javase/tutorial/deployment/deploymentInDepth/jnlpFileSyntax.html

Example JNLP File:
```
<?xml version="1.0" encoding="UTF-8"?>
<jnlp spec="1.0+" codebase="" href="">
    <information>
        <title>Dynamic Tree Demo</title>
        <vendor>Dynamic Team</vendor>
        <icon href="sometree-icon.jpg"/>
        <offline-allowed/>
    </information>
    <resources>
        <!-- Application Resources -->
        <j2se version="1.6+" href=
           "http://java.sun.com/products/autodl/j2se"/>
<!--        <jar href="https://docs.oracle.com/javase/tutorialJWS/samples/deployment/dynamictree_webstartJWSProject/DynamicTreeDemo.jar" main="true" /> -->
        <jar href="https://joshuastringfellow.com/webTesting/DynamicTreeDemo.jar" main="true" />

    </resources>
    <application-desc
         name="Dynamic Tree Demo Application"
         main-class="webstartComponentArch.DynamicTreeApplication"
         width="300"
         height="300">
     </application-desc>
     <update check="background"/>
</jnlp>
```

#### Setting up the Jar/App
