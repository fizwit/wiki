---
title: Shiny Applications
last_modified_at: 2018-06-20
---

# Introduction

Shiny is an R package that makes it easy to build interactive web apps straight from R. You can host standalone apps on a webpage or embed them in R Markdown documents or build dashboards. You can also extend your Shiny apps with CSS themes, htmlwidgets, and JavaScript actions. For more information about Shiny, [go to Rstudio's Shiny page.](https://shiny.rstudio.com)

## Options to deploy Shiny App
1. Using Shinyapps.io to deploy Shiny Apps
2. Using Application deployment pipeline developed by Hutch Scientific Computing

- Pros of Using Shinyapps.io to deploy Shiny Apps
    - It streamlines with RStudio. 
    - The free plan with **25 hours activity per month**. 
    - The ‘standard’ plan including password protection costs **$99/month**.
    - The ‘professional’ plan including password protection and costom domain/url costs **$299/month**.
    - Deploying shiny apps on Shinyapps.io allows you to include multiple applications within a single GitHub repository, which is not available with SciComp’s pipeline. 
    - Shinyapps.io also provides web analytics feature showing app activities. 
    - The auto-deployment occurs within RStudio by clicking one while the SciComp’s pipeline auto-deployment occurs at pushing codebase changes to remote GitHub repo. 

- Pros of Using Application deployment pipeline developed by Hutch Scientific Computing:
    - SciComp’s pipeline is more generic than Shinyapps.io can offer. As the later provides a streamlined deployment service with a cost. The former has capacity of hosting applications written in other languages as long as the application itself can be containerized. 
    - Integration with data sources within Hutch campus. For example, the application can be connected to a campus based database system (Postgres, mysql, etc…) without exposing it to the entire internet. 
    - There is a template repository (https://github.com/FredHutch/shiny-app-template) to help users to assemble your own shiny app
    - Once the application is deployed, no manual deployment is required when new changes are made as the pipeline includes continuous integration/continuous delivery (CI/CD) feature. 
    - Users can pick their own custom site URL in the fredhutch.org domain (example: 'myshinyapp.fredhutch.org')"
    - User can specify if their app is only facing campus within the firewall or being exposed to the entire internet. Authorization feature can also be included upon request. 
    - The last one is, all the features mentioned above are completely free to campus users. 

## Prerequisit of using SciComp deployment pipeline:
- Use Github as version control system
- Do NOT want to pay 
- Comfortable of using command line with understanding the meaning or not

# SciComp App Deployment Pipeine Tutorial

## GitHub Setup
To deploy a Shiny app via the Fred Hutch system, you must first have access to the Fred Hutch institution GitHub.  [You can find GitHub instructions in this demo.](https://fredhutch.github.io/wiki/compdemos/comp_github/)

## Download the Template
The template for your app can be found in this GitHub Repo (accessible after login):
[FredHutch/Shiny-app-template](https://github.com/FredHutch/shiny-app-template)

### Using Command Line Git
![]({{ site.baseurl }}/compdemos/assets/com-com.png)
```
    git clone https://github.com/FredHutch/shiny-app-template.git <your_app_folder>
    cd <your_app_folder>
    ls -al
    rm -rf .git
    ls -al
    git init
    echo "# <your_app_folder>" > README.md
    git add .
    git commit -m 'initial commit'
```
After the steps above from a terminal, you have achieved these steps:
- Cloned a template
- Created your own repo
- Add a new git control to this repo

Now it's time to inject your wonderful shiny app to this template. The goal is to put all your app code base to template's subfolder 'app'.  

### Using the GitHub Desktop Application

To keep track of file changes within a local repo, first add this folder to GitHub Desktop Application:
![]({{ site.baseurl }}/compdemos/assets/electro-add-repo.png)
![]({{ site.baseurl }}/compdemos/assets/rsz_1electron-add-repo-2.png)

You can create a remote repo by clicking on the 'Publish repository' and select the correct branch (in this case 'master' is the branch name). You can specify if you want this repo to be private or not. Also, please make sure this repo is under FredHutch as the organization.
![]({{ site.baseurl }}/compdemos/assets/electro-create-remote-repo.png)

## Insert Your App into the Template
Use your favorite code editor to add your own shiny app content to this template.  Here are a few reminders for the shiny apps with a single R script:

- Please split your app.R to ui.R and server.R according to the template app subfolder's file structure.
- Make sure you include 'library(shiny)' to both ui.R and server.R files
- In server.R, please remove 'shinyApp(ui, server)'
- You can add your data to a data folder under app folder

## Push Edits to GitHub
After you added your own content to this repo, you are ready to commit the changes and push the changes to the remote repo.

- Now your GitHub Desktop Application console looks like this:
![]({{ site.baseurl }}/compdemos/assets/electron-before-commit.png)

- Two files with green crosses on the right have been added as new files.
Two existing files have been modified with yellow dots on the right.
You can further examine and adjust those changes by click the yellow dot or right click:
![]({{ site.baseurl }}/compdemos/assets/electron-mod.png)

- Writea commit message and click on 'commit to master' if you want to commit change to your master branch:
![]({{ site.baseurl }}/compdemos/assets/electron-com.png)

- Push committed change from local files to remote repo
![]({{ site.baseurl }}/compdemos/assets/electron-push.png)

## Viewing Your App
You should be able to find your app within the repo you created
![]({{ site.baseurl }}/compdemos/assets/github-repo_s.png)

<!--Please also add topics 'r' and 'shiny'
![](/{{ site.baseurl }}/compdemos/assets/GitHub-add-labels-3.png)-->

## Test Your Application Locally
Open the app in an R console.
![]({{ site.baseurl }}/compdemos/assets/r.png)

- Change directory to subfolder 'app' under your app root:
``` 
    cd <your_app_folder>
    cd app
    R
```
- Via R console, 
``` 
    source('start.r') 
```

- Then go to a browser to check the url: http://localhost:7777



## Deployment Service from SciComp
Hopefully, you can see your app working as expected in the browser. Please keep a good record of all your dependencies. You may have all the necessary R packages installed on your local machine but SciComp deployment platform needs to know those dependencies.  You also want to be ready to answer all the questions below before you contact Scientific Computing team.  If you feel ready with your **codebase** as well as the **below information required by deployment**, contact Scientific Computing at `scicomp` to start the process of deploying your application on a server so others can access it.

1.  Is your application codebase version-controlled by Git and in a GitHub repository (repo) ?  If so, is it under FredHutch account?

2. How do you want to name (DNS name) your application? So the it will look something like <your_application_DNS_name>.fredhutch.org

3. Is your application facing Fred Hutch **internally** (open to the Fred Hutch campus) or **externally** (open to the entire internet)?

4. Does your application require authorization (password protection), that only your collaborators have access?

5. Does your application contain PHI? Please remove PHI from your application?

6. Please list out all the dependencies (R packages you used).


## Available Resources
- [Introduction to Shiny with a cheatsheet and some example apps](http://zevross.com/blog/2016/04/19/r-powered-web-applications-with-shiny-a-tutorial-and-cheat-sheet-with-40-example-apps/)
- [How to get started with Shiny apps](https://shiny.rstudio.com/articles/build.html)
- [Which GitHub protocol should I use?](https://gist.github.com/grawity/4392747)
- [Tutorial](http://shiny.rstudio.com/tutorial/)
- [Shiny cheatsheet](http://shiny.rstudio.com/images/shiny-cheatsheet.pdf)
- [Shiny articles](http://shiny.rstudio.com/articles/)
- [Show me shiny](http://www.showmeshiny.com/)
- [Shinyapps.io](http://www.shinyapps.io/)
- [Gallery](http://shiny.rstudio.com/gallery/google-charts.html)
- [Shiny Google User Group](https://groups.google.com/forum/#!forum/shiny-discuss)