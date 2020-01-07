FROM ubuettgen/alpine-jetty9 
MAINTAINER Ulrich Büttgen  "ulrich@buettgen.org"

RUN wget http://dl.bintray.com/jfrog/artifactory/artifactory-3.3.0.zip
RUN unzip artifactory-3.3.0.zip
RUN mv artifactory-3.3.0/webapps/artifactory.war /opt/jetty/webapps
RUN rm artifactory-3.3.0.zip
RUN rm -rf artifactory-3.3.0

