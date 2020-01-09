#start with base tomcat container
From tomcat
RUN apt-get update

# Install maven and git to download and build project for the artifact
RUN apt-get install -y maven
RUN apt-get install -y git

#download projet
RUN git clone https://github.com/efsavage/hello-world-war.git /hello-world

#build maven for project
WORKDIR /hello-world
CMD ["mvn",  "package"]

#copy artifact to tomcat
RUN cp /hello-world/dist/hello-world.war /usr/local/tomcat/webapps/hello-world.war

#start tomcat
CMD ["catalina.sh", "run"]

#note start docker with -p 8080:8080 option to expose tomcat on port 8080 on host machine