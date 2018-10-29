---
title: "Configuring JNDI Mail Session in Tomcat"
date: 2009-12-07T21:42:15+11:00
draft: false
---

I've just joined a project as a freelancer to customize a commercial e-commerce solution (so let called it EP). OOTB, the email sending of EP does not support authentication, which is a weird thing for such a cool product like that. Actually, EP does declare an JNDI mail session in the context, but in the code they don't use it. With the source code of EP in hand, things get much easier. First, we declare a JNDI resource in our application context (either in your context file in the `conf/Catalina/localhost/` or in your `context.xml` under `META-INF` inside your war):

```xml
<context>
    <Resource name="mail/Session" 
              auth="Container"
              type="javax.mail.Session"    
              username="my.smtp.user"
              password="my-secret"
              mail.debug="false"
              mail.transport.protocol="smtp"
              mail.smtp.host= "xxx.xxx.xxx.xxx"
              mail.smtp.auth= "true"
              mail.smtp.port= "25"
              mail.smtp.starttls.enable="true"
              description="Global E-Mail Resource">
              
    </Resource>
</context>
```

And put those in your `web.xml` file:

```xml
<resource-ref>
    <description>Email Session</description>
    <res-ref-name>mail/Session</res-ref-name>
    <res-type>javax.mail.Session</res-type>
    <res-auth>Container</res-auth>
</resource-ref>
```

And now, in your Java code, you will use this email session like this:
```java
    Context initContext = new InitialContext();
    Context context = (Context) initContext.lookup("java:comp/env");
    Session mailSession = (Session) context.lookup("mail/Session");
    //Your code to send the email goes here
```

If you get a `java.lang.ClassCastException`, don't worry, this is a known issue. It's because you have multiple Java Mail jar file and Java Activation Framework jar file in your CLASSPATH!

Hope that may help!