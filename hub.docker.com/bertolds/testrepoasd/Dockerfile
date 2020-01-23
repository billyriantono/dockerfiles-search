FROM maven:3.3-jdk-8

VOLUME /tmp

WORKDIR /

# Prepare by downloading dependencies
ADD pom.xml /pom.xml 
#RUN ["mvn", "dependency:resolve"]
#RUN ["mvn", "verify"]

# Adding source, compile and package into a fat jar
ADD src /src
RUN ["mvn", "clean", "install"]

RUN ["ls", "/target"]
RUN ["pwd"]
RUN ["ls", "-ltrh", "/target/MS-HelloWorld_basic-0.0.1-SNAPSHOT.jar"]

EXPOSE 8080

ENTRYPOINT [ "java", "-jar", "/target/MS-HelloWorld_basic-0.0.1-SNAPSHOT.jar" ]