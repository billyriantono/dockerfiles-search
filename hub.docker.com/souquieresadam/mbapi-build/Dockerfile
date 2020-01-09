#from a Java 8 
FROM java:8 

# Install maven
RUN apt-get update  
RUN apt-get install -y maven

WORKDIR /code

# Prepare maven
ADD pom.xml /code/pom.xml  


# Adding source, compile and package
ADD src /code/src  
RUN ["mvn", "package"]

CMD ["/usr/lib/jvm/java-8-openjdk-amd64/bin/java", "-jar", "target/mbapi-0.5.jar"] 