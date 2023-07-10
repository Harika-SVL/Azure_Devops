## Big Bang integration
* Consider a case where you are working for vintage systems where we are developing ecommerce application in Waterfall model

![Alt text](shots/1.PNG)

* Application is in layered architecture

![Alt text](shots/2.PNG)

* We have team managers
   1. Andy
   2. Brian
   3. Cathy

![Alt text](shots/3.PNG)

* Project has to be finished in an year
* Each team works independently for 9 months and finishes the devlopment

![Alt text](shots/4.PNG)

* Big Bang integrations are error prone, so best solution would be continuos integration (CI).
* The Goal of CI is to inform dev teams about the failures of integration.
* To perform CI different tools started like cruise control and hudson/jenkins
* Need for automated tests/unit tests started at this point.

## Agile way of Software Development

* Agile had added smaller and frequent releases, this needs more aggressive automations than CI.
* Expectation:
  * Automated Pipeline which when developer pushes changes
      * Build/Package code
      * Code Quality and Security Issues
      * Automate test executions with System, Performance, Reliablity, Security
      * Report of the Quality of work done yesterday
  * Customer and Internal Releases every 2 weeks

## Quick Overview of Continuous Delivery Pipeline

* Overview

![Alt text](shots/5.PNG)

* This pipeline will be triggered by the changes in the Version Control Systems (VCS)

## WOW (Ways of Working)

* Figure out the manual steps
* Implement manual steps in Pipeline depending on your ci/cd engine
* Steps for gameoflife Refer Here
* Softwares requried
    * git
    * jdk 8
    * maven

* Manual steps :

![Alt text](shots/6.PNG)
![Alt text](shots/7.PNG)
![Alt text](shots/8.PNG)

* Pipeline in Jenkins
```
pipeline {
    agent any
    stages {
        stage ('vcs') {
            steps {
                git 'https://github.com/wakaleo/game-of-life.git'
            }
        }
        stage ('build') {
            steps {
                sh 'mvn package'
            }
        }
    }
}
```
* Pipeline in Azure DevOps
```
steps:
- task: Maven@4
  inputs:
    mavenPomFile: 'pom.xml'
    goals: 'package'
```
## Git

* Git is a Distributed Version Control System
* Git is Hosted by many providers
    * GitHub
    * Azure Source Repos
    * Code Commit
    * Bit Bucket
    * Git Lab

## Git-Basics

* Scope of the current discussion would be on how to submit the changes to the Git Repository and how to get latest changes from git repository
* Workflow
    * Setting up a GitHub Account
    * Setting up a user details and credentials (key based credentials)
    * Creating a Git Repository, Adding code/docs submitting to the repository

## Git Workflow

[ Note: This is a partial workflow and we will be learning complete git in 2 weeks from now ]

* Git Remote Repositories are hosted by GitHub/GitLab/Azure Source Repos etc
* If we don’t have the Code in local system, then we clone the code to create local repo
* Once we have local repo, to get latest changes we use pull
* We add the changes to the staging area using 'git add .' and commit the changes to local repo using 'git commit -m "Added changes" ' and sync the changes from local to remote repo using 'git push origin main' commands

![Alt text](shots/9.PNG)

#### Create a Git Repository in GitHub

* Create a new repository after login into github

#### Cloning the code into local system

* Identify a folder for local repo '<local repo location path>'
* Now clone using a command 'git clone <git-url>' command
* Let's look into what are the contents using 'ls' command

#### Make changes locally and push to the Remote

* Add the changes in working tree and then add to staging area.
* Commit the changes and push to the remote

![Alt text](shots/10.PNG)

* Adding multiple changes
    * Files already in repo will have status of modified or deleted or renamed
    * Files newly created will have status of untracked

![Alt text](shots/11.PNG)

* we can add multiple changes at once to the staging area
* When we want to move the changes from staging area to local repo, it needs message, author username and email address

#### Get changes from remote into local when repo already exists

* Use pull

![Alt text](shots/12.PNG)

* Git ways of working in non-tech way

![Alt text](shots/13.PNG)

## Branches in Git

* Git allows us to work parallely for different use cases
    * multiple versions of same application
    * multiple customers for same application

![Alt text](shots/14.PNG)

* HEAD is a pointer which generally points to a branch
* HEAD can be moved from one branch to other using a command called as 'CHECKOUT'
    * We execute 'git checkout v1.0'

![Alt text](shots/15.PNG)

* Let's work with branches using nopcommerce [Refer here : 'https://github.com/nopSolutions/nopCommerce/branches']

![Alt text](shots/16.PNG)

* Moving from one branch to other

![Alt text](shots/17.PNG)

* Things to digest
    * default branch: master
    * default remote: origin
    * remote branch: name of remote/name of branch
* Single local repo can have multiple remote repo's

### Building and Packaging the code

* Building the code and packaging the code to the suitable format for end deployment is very technology specific i.e. it is different depending on programming languages
* Programming Languages can be categorized into 3 formats
    * Compiler based

     ![Alt text](shots/18.PNG)

    * Interpreter based

     ![Alt text](shots/19.PNG)

    * Hybrid

     ![Alt text](shots/20.PNG)

## Building and Packaging Code

### Dependecny Management

* To develop any application , there will be lots of dependencies on other libraries/sdks(Software developmet kit)
* Before building/packaging we need to download these dependencies
    * nodejs - npm
    * python - pip
    * .net - nuget
    * java - mvn

### Test Executions

    * We would be running
        * unit tests (test code by writing code) => developers
        * integration tests
            * unit test
            * ui test
            * api test
        * Functional tests
            * ui tests (simulate user) => selenium, cypress, qtp…
            * api tests (postman, rest assured)
        * Performance tests:
            * load testing harness (jmeter, load runner)
* What we should know for ci/cd
        * command to invoke tests
        * where will be test results
        * converting test results to some common formats (junit xml)

### Java Based Applications

* To build Java Based applications, we have many tools
    * ANT
    * Maven
    * Gradle
* In this case we will be using a maven based java application
    * JDK = 17
    * MVN 3 +
    * Project: [ Refer Here : 'https://github.com/spring-projects/spring-petclinic' ]
* Manual steps : 
```
sudo apt update
sudo apt install openjdk-17-jdk -y
sudo apt install maven -y
git clone https://github.com/spring-projects/spring-petclinic.git
cd spring-petclinic
mvn package                     # Builds code, Creates package, Runs unit tests
```

### .net framework versions:

    * .net 2,3,4 (Windows)
    * .net 5 +
        * .net core
        * aspnet core
* Build the nopcommerce [ Refer Here : 'https://github.com/nopSolutions/nopCommerce' ]
* Softwares:
    * .net core 7 [ Refer Here : 'https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu-2204' ]
```
sudo apt-get update && \
  sudo apt-get install -y dotnet-sdk-7.0
```
* Build steps :
```
git clone https://github.com/nopSolutions/nopCommerce.git
cd nopCommerce
git checkout master
dotnet restore src/NopCommerce.sln
dotnet build src/NopCommerce.sln
```

## Azure DevOps

* Azure DevOps offers services to manage whole project
    * Project Management
        * Planning
            * Agile Boards
            * Issue Tracker
        * Execution
            * Wiki Pages
            * Test Management
    * DevOps:
        * VCS:
            * Azure Source Repos
                * Git
                * TFVC
        * Pipelines:
            * Build Pipelines
            * Release Pipelines
        * Artifacts
* Azure DevOps can be used by two ways
    * Self-Hosted [ Refer Here : 'https://learn.microsoft.com/en-us/azure/devops/server/download/azuredevopsserver?view=azure-devops' ]
    * Cloud Hosted: [ Refer Here : 'https://azure.microsoft.com/en-in/products/devops' ]
* Azure DevOps Services: Cloud Hosted Version of Azure DevOps
    * Pricing: [ Refer Here : 'https://azure.microsoft.com/en-in/pricing/details/devops/azure-devops-services/' ]
* Create a free azure devops account [ Refer Here : 'https://azure.microsoft.com/en-in/products/devops' ]



### Importing an Existing git repo into Azure DevOps

* Import Repository from github into your account




* Now lets setup build i.e. CI pipeline










* By default Parallelism request is disabled we need to enable this by sending request to microsoft on this location [ Refer Here : 'https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbR63mUWPlq7NEsFZhkyH8jChUMlM3QzdDMFZOMkVBWU5BWFM3SDI2QlRBSC4u' ]

[ Note: [ Refer Here : 'https://www.youtube.com/watch?v=ggOmHlnhPaM&list=PLuVH8Jaq3mLud3sVDvJ-gJ__0zd15wGDd&index=16' ] for YAML and JSON Tutorial ]