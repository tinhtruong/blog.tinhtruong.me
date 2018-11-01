---
title: "How to import Git Projects from Bitbucket into Eclipse"
date: 2012-03-28T22:03:20+11:00
draft: false
tags: ["bitbucket", "eclipse", "git"]
---

This how-to is served as my memo to import a Bitbucket project into Eclipse. First things first, make sure you have an up-and-running Eclipse with EGit (in this how-to I am using Eclipse Indigo 3.7.2 with EGit 1.3.0)


* Create a folder to hold the workspace for your new project (You can skip this step if you want to use an existing workspace), I will use one of my project on Bitbucket in this how-to. It's GreenMail web application. So I create a folder name **greenmail-webapp**
* Open the Git Repositories view (it's under Windows -> Show View -> Other..., then under the Git category). 
* Click **Clone a Git repository** and paste in the whole Git repo URL to the URI textbox, EGit will automatically fill in other textbox with the right value (so cool!), all you need is to enter the correct password. Then click *Next*.

    ![Git repo view](http://4.bp.blogspot.com/-n6WkcrEEbvY/T3JTQpzlOFI/AAAAAAAAALs/W9i1d45xr-Q/s1600/git-repo-view-crop.png "Git repo view") 
* At the **Branch Selection** screen you are able to choose a branch to clone, my project has only one branch (master). If you clone an empty project from Bitbucket, just click *Next*.
![Choose branch](http://2.bp.blogspot.com/-bevye3Srzxw/T3JT0snjz0I/AAAAAAAAAL4/BTrF-3BUC4A/s1600/choose-branch.png "Choose branch") 
* At the **Local Destination**, browse to your workspace directory for this project. I usually don't check-in the **.project** and **.classpath** files into the VCS, I just generate them locally right after I checkout/clone instead. If your build tool does not generate those files for you or you are the only one in this project, it'd better to check-in those files.
![Local destination](http://4.bp.blogspot.com/-_jBwB4Cfaqw/T3JUAVbCyvI/AAAAAAAAAME/JnsQipQ8_6s/s1600/local-destination.png "Local destination")

* Now, let's generate the Eclipse project files. I use Gradle as my build system, so it's just a command away.
    ```shell
    gradle eclipse
    ``` 

    Before running this, make sure you've already applied the `eclipse` plugin in your **build.gradle**. If you use Maven, please include the maven-eclipse-plugin into your **pom.xml** and run the command
    ```shell
    gradle eclipse:eclipse
    ```  
The above commands will generate/overwrite the *.project* and *.classpath* for you. 

* Returning to your Eclipse, you can now Import your new cloned project into your workspace by right clicking on your in the Git Repository view, select Import Projects...
![Import project](http://3.bp.blogspot.com/-Ivb6KvIKYbM/T3Jix-MrMuI/AAAAAAAAAMc/v_Ue33yLyEI/s1600/import-project.png "Import project")

* Select **Import existing projects**
![Import Project From Repository](http://4.bp.blogspot.com/-pFUhxldyPG4/T3Jh0vkpyxI/AAAAAAAAAMQ/3ld5qK5DMNw/s1600/Import%2BProjects%2Bfrom%2BGit%2BRepository.png "Import Project From Repository")

* Select the project you want to import. 
![Existing projects](http://3.bp.blogspot.com/-74tG1Hw5OKI/T3Ju682_SKI/AAAAAAAAAMo/jGalzuo2vEo/s1600/existing-projects.png "Existing projects")

Happy coding!

