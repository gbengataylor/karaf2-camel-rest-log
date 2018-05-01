
forked and modified from [quickstart](https://github.com/fabric8-quickstarts/karaf2-camel-log)


# Karaf 2 Camel Log QuickStart

This quickstart shows a simple Apache Camel Karaf 2 application deployed on OpenShift that logs a message to the server log every 5th second.

This example is implemented using solely the XML DSL (there is no Java code). The source code is provided in the following XML file `src/main/resources/OSGI-INF/blueprint/camel-log.xml`.
It also shows how Karaf assembly files can be overriden using resources from `src/main/resources/assembly/`. In the included sample log file `etc/org.ops4j.pax.logging.cfg` uncommenting the following line will enable verbose Camel log messages

    #log4j.logger.org.apache.camel=DEBUG


## Pre-requisites 

### Download the required FIS 2.0 Karaf images 

    oc create -n openshift -f https://raw.githubusercontent.com/jboss-fuse/application-templates/fis-2.0.x.redhat-R6/fis-image-streams.json

Admin rights are required to create in the openshift namespace


### Upload the template 

    oc create -n openshift -f karaf2-camel-rest-log-template.json

if it already exists

    oc replace -n openshift -f   karaf2-camel-rest-log-template.json
    		
Admin rights are required to create/replace in the openshift namespace

## Running the example in OpenShift using template

Create the following environment variables. Make the appropriate modifications

    export OPENSHIFT_CAMEL_NO_AMQ_APPLICATION_NAME=fis-karaf-camel-rest-log-route

    export GIT_REPO_CAMEL_NO_AMQ=https://github.com/gbengataylor/karaf2-camel-rest-log.git
    
    export IMAGE_BUILD_VERSION=2.0

Deploy the camel route 

    oc new-app --template= karaf2-camel-rest-log app=${OPENSHIFT_CAMEL_NO_AMQ_APPLICATION_NAME} --param  APP_NAME=${OPENSHIFT_CAMEL_NO_AMQ_APPLICATION_NAME} --param GIT_REPO=${GIT_REPO_CAMEL_NO_AMQ}  --param SERVICE_NAME=${OPENSHIFT_CAMEL_NO_AMQ_APPLICATION_NAME}  --param BUILDER_VERSION=${IMAGE_BUILD_VERSION} --param GIT_REF=master  -l app=${OPENSHIFT_CAMEL_NO_AMQ_APPLICATION_NAME}



