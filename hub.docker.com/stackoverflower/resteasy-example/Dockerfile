FROM stackoverflower/java7-tomcat7-maven3:1.0

MAINTAINER rju

# First copy pom.xml to /project
ADD pom.xml /project/

RUN mkdir /project/src/

# Next resolve Maven dependencies.  This is so that if the pom.xml has not changed, then this will run from cache instead of actually downloading the dependencies
RUN cd /project/ && mvn clean compile

ADD src /project/src/

RUN cd /project/ && mvn clean install && cp target/docker-restaesy-1-1.0.0-SNAPSHOT.war /tomcat/webapps/api.war && rm -r /root/.m2

EXPOSE 8080

ENTRYPOINT ["/run.sh"] 
