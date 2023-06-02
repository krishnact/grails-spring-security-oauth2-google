Spring Security OAuth2 Google Plugin
====================================

***What version of Grails is this compatible with?***

I have used it with Grails 5.3.2

***How to build and publish to local maven?***
```shell
.\gradlew clean build publishToMavenLocal
```

[ ![Download](https://api.bintray.com/packages/grails/plugins/spring-security-oauth2-google/images/download.svg) ](https://bintray.com/grails/plugins/spring-security-oauth2-google/_latestVersion)

Add a Google OAuth2 provider to the [Spring Security OAuth2 Plugin](https://github.com/grails-plugins/grails-spring-security-oauth2).

***How to use in Grails?***

Installation
------------
Add the following dependencies in `build.gradle`
```
dependencies {
...
    implementation 'org.grails.plugins:spring-security-oauth2:2.0.0-RC1'
    implementation "grails.spring.security.oauth2:spring-security-oauth2-google:1.5.1.BUILD-SNAPSHOT"
...
}
```
***What else do I need to configure in my app?***

You need to define these four values in application.groovy:
* grails.plugin.springsecurity.userLookup.userDomainClassName
* grails.plugin.springsecurity.userLookup.authorityJoinClassName
* grails.plugin.springsecurity.authority.className
* grails.plugin.springsecurity.oauth2.domainClass

example:
grails.plugin.springsecurity.oauth2.domainClass = 'com.yourapp.OAuthID'

For defining classes please look here:
https://github.com/dhirajbadu/grails4_oauth2_social_login/tree/main/grails-app/domain/com/yourapp


Usage
-----
Add this to your application.yml
```
grails:
    plugin:
        springsecurity:
            oauth2:
                providers:
                    google:
                        api_key: 'google-api-key'               #needed
                        api_secret: 'google-api-secret'         #needed
                        successUri: "/oauth2/google/success"    #optional
                        failureUri: "/oauth2/google/failure"    #optional
                        callback: "/oauth2/google/callback"     #optional
                        scopes: "some_scope"                    #optional, see https://developers.google.com/identity/protocols/googlescopes#monitoringv3
```
You can replace the URIs with your own controller implementation.

In your view you can use the taglib exposed from this plugin and from OAuth plugin to create links and to know if the user is authenticated with a given provider:
```xml
<oauth2:connect provider="google" id="google-connect-link">Google</oauth2:connect>

Logged with google?
<oauth2:ifLoggedInWith provider="google">yes</oauth2:ifLoggedInWith>
<oauth2:ifNotLoggedInWith provider="google">no</oauth2:ifNotLoggedInWith>
```
License
-------
Apache 2
