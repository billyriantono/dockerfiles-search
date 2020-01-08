# latest of tomcat v9 with JRE 11 is the basis
FROM tomcat:9-jre11

# set maintainer
MAINTAINER Murat Artim "muratartim@gmail.com"

# copy war
COPY target/EclipseTacticsWeb-*.war /usr/local/tomcat/webapps/EclipseTacticsWeb.war

# To build the docker image: (from where this file is located)
# docker image build -t muratartim/eclipsetactics_web_server:latest .

# To create & run the container:
# docker container run -p 8080:8080 -d --name eclipsetactics_web_server --network eclipsetactics_network muratartim/eclipsetactics_web_server

# To start an existing container
# docker container start eclipsetactics_web_server