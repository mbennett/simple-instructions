# simple-instructions
Instructions for running the simple-gateway and simple-service on PWS (and local)

## Clone
First clone my repos.
- simple-config-files
- simple-config-server
- simple-discovery-server
- simple-gateway
- simple-service

## Run Locally
- Start simple-discovery-server
- Start simple-config-server providing a value for **simple.config.repo.location** property using one of these methods:
    * -Dsimple.config.repo.location=file:///Users/yourUserName/path/to/simple-config-files on the command line
    * in your STS/Eclipse run configuration
    * or whatever
- Start simple-service
- Hit http://localhost:8081/ and make sure you get the message "Hello! The testMessage is: test message for **default** profile"
- Start simple-gateway
- Hit http://localhost:9090/api/simple/ and make sure you get the message "Hello! The testMessage is: test message for **default** profile"

## Deploy to PWS
**WARNING:** there are costs when running on PWS.  Very minimal though.
- Run mvn clean install for simple-service
- Run mvn clean install for simple-gateway
- In the PWS Marketplace choose "Config Server" and name the instance "config-server"
    * There is a configuration that needs to be done only once.  I will leave that exercise to you.
    * http://docs.pivotal.io/spring-cloud-services/1-5/common/config-server/configuring-with-git.html will get you started
- Wait a bit for the service to install
- In the PWS Marketplace choose "Service Registry" and name the instance "service-registry"
- Wait a bit for the service to install
- Push simple-service to PWS using one of these methods
    * cf cli
    * STS integration
    * or whatever
- Visit the random route URL (like https://simple-service-uijlggon.cfapps.io/) and make sure it returns "Hello! The testMessage is: test message for **dev** profile"
- Push simple-gateway to PWS using whatever method
- Visit the random route URL (like https://simple-service-uijlggon.cfapps.io/api/simple/) and make sure it returns "Hello! The testMessage is: test message for **dev** profile"
    * FYI I tried a path of /api/simple without the trailing forward slash and got an error.  Not sure why yet.

That's it!  Thanks.  Let me know if you have issues.
