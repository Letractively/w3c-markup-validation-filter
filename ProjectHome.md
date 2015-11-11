# What is it #

This project provides the `W3cMarkupValidationFilter`, which

  * captures the HTML of all rendered pages
  * Sends the HTML to a W3C Markup Validation Service
  * Injects a little box into the HTML page, which becomes green, if the HTML is valid, or otherwise red

The injected box also contains a link to the validation result page, where you can see a detailed description for each error.

# Quickstart #

1.) Download http://w3c-markup-validation-filter.googlecode.com/files/W3cMarkupValidationFilter-1.0.2.jar

2.) If you use Maven, you can install the jar file into your local repository via
```
    mvn install:install-file -DgroupId=de.michaeltamm \
                             -DartifactId=W3cMarkupValidationFilter \
                             -Dversion=1.0.2 \
                             -Dpackaging=jar \
                             -Dfile=/path/to/downloaded/W3cMarkupValidationFilter-1.0.2.jar
```
and then add the following dependency to your pom.xml
```
    <dependency>
        <groupId>de.michaeltamm</groupId>
        <artifactId>W3cMarkupValidationFilter</artifactId>
        <version>1.0.2</version>
    </dependency>
```
If you don't use Maven, add the jar file to your `WEB-INF/lib` directory as well as the following jar files, which the `W3cMarkupValidationFilter` depends on:
  * http://repo2.maven.org/maven2/commons-httpclient/commons-httpclient/3.1/commons-httpclient-3.1.jar
  * http://repo2.maven.org/maven2/commons-logging/commons-logging/1.0.4/commons-logging-1.0.4.jar
  * http://repo2.maven.org/maven2/commons-codec/commons-codec/1.2/commons-codec-1.2.jar

3.) Add the following snippet to your `web.xml`
```
    <filter>
        <filter-name>W3cMarkupValidationFilter</filter-name>
        <filter-class>de.michaeltamm.W3cMarkupValidationFilter</filter-class>
    </filter>

    <filter-mapping>
        <filter-name>W3cMarkupValidationFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

```
4.) Deploy your web application on to a local servlet container, start it and request any page - the little box should appear in the upper right corner of your browser.

# You should also ... #

By default, the `W3cMarkupValidationFilter` uses the publicly available W3C Markup Validation Service under the URL http://validator.w3.org/

You might want to install the W3C Markup Validation Service on a server in your intranet and configure the `W3cMarkupValidationFilter` in your `web.xml` like this:
```
    <filter>
        <filter-name>W3cMarkupValidationFilter</filter-name>
        <filter-class>de.michaeltamm.W3cMarkupValidationFilter</filter-class>
        <init-param>
            <param-name>enabled</param-name>
            <param-value>true</param-value>
        </init-param>
        <init-param>
            <param-name>checkUrl</param-name>
            <param-value>http://your.server/path-to-validator/check</param-value>
        </init-param>
    </filter>
```

When deploying your web application on to a production environment, you can either remove the `<filter>` and its `<filter-mapping>` from the `web.xml` or set the `init-parameter` enabled to `false`.