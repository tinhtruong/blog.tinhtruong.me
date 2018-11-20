---
title: "How to Install Gradle Templates Plugin Globally"
date: 2012-01-28T23:21:54+11:00
draft: false
---

I've been exposing to Gradle for a couple of weeks and really like it. As a Maven user, I found that Gradle is a refreshing methodology on how a build tool should be. But one thing I miss from the Maven land: the ability to generate the initial structure for a project (I mean the 'archetype' plugin of Maven). Luckily, due to the plugin architecture of Gradle, [a Gradle user](http://eric-berry.blogspot.com) has developed a plugin just for that purpose. It's called the `templates` plugin. The [wiki](http://tellurianring.com/wiki/gradle/templates) page of the plugin gives you all the details you need to install, but the global installation section is confusing and did not work. Here is how I did to make it work: 

* Create a file called `templates.gradle` in the _~/.gradle/init.d/_ folder (actually you can name it whatever you want as long as it has the extension .gradle)
* Edit that file and paste this little code snippet:


    ```groovy
    gradle.beforeProject { prj ->
        prj.apply from: 'http://launchpad.net/gradle-templates/trunk/latest/+download/apply.groovy'
    }
    ```
Now, you can create a project structure event without a build.gradle with the command:
    
    ```shell
    gradle createJavaProject
    ``` 
Happy coding!