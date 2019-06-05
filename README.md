# ci-project

## Components 
The goal of this project is to set up a continuous integration pipeline for an application that provides secure login functionality. The app consists of 14 components: 
*	1 gateway: this uses nginx to route traffic to the other components.
*	2 Clients: these are the webpages written with VueJS.
*	10 Services: these are the APIs for the app written in nodeJS. 
*	1 Database: this app uses mongo as its database.

## Architecture
![Architecture map](https://github.com/wrusselly/ci-project/blob/master/CI-project.png)

Above is the architecture map for this project. Each component depends on any downstream components(e.g. email-service depends on mongo-service), so when building it must be done from the bottom up. Currently the role and group service are not connected to the rest of the application. All requests from the user pass through the gateway which then routes them to the appropriate place. 


## Docker-Compose Set-up 
### Prerequisites:
* Docker 
* Docker compose 
* Git 
* Gmail account with insecure apps enabled. 

### Steps: 
**1.**	Create an environment variables file and source the file where the project will be built. The email service takes 3 environment variables (GMIAL_USER, GMAIL_PASS, SERVICE_NAME)and the authentication service takes one (ACTIVATION_LINK). An example file is below: 

    GMAIL_USER=example@gmail.com                                  #the account that will send activation emails 
    GMAIL_PASS=password                                           #the password for the account 
    SERVICE_NAME="my project"                                     #the name of the project that will appear on the email 
    ACTIVATION_LINK=http://localhost/authentication/api/activate  #the link that will be sent to users to activate their accounts 

**2.**	Clone the project from git https://github.com/wrusselly/ci-project.git. Change into the ci-project-dist directory, where the docker-compose.yaml is. `Run docker-compose up –d`  


