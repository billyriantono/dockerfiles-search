# Pull Base Image
FROM java:8

#Install MAven
RUN apt-get update
RUN apt-get install -y maven

#Add Code to Docker Iamge
ADD /HelloWorld /app/HelloWorld
ADD /JunitTesting /app/JunitTesting
ADD pom.xml /app/

#set working directory
WORKDIR /app/HelloWorld

#Run Maven to build Code
RUN ["mvn", "clean", "install"]

#Run the jar
CMD ["java","-cp","target/HelloWorld-0.0.1-SNAPSHOT.jar","com.kdp.java.HelloWorld"]

