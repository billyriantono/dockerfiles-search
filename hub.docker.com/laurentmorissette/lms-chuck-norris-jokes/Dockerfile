#source article http://whitfin.io/speeding-up-maven-docker-builds/
FROM maven:3.5-jdk-8 as maven
MAINTAINER "laurent.morissette@gmail.com"
# copy the project files
COPY ./pom.xml ./pom.xml

# build all dependencies
RUN mvn dependency:go-offline -B

# copy your other files
COPY ./src ./src

# build for release
RUN mvn package

# our final base image
FROM openjdk:8-jdk-alpine

# set deployment directory
WORKDIR /tmp

# copy over the built artifact from the maven image
COPY --from=maven target/norris-jokes-*.jar ./norris-jokes.jar
EXPOSE 8080
# set the startup command to run your binary
CMD ["java", "-jar", "norris-jokes.jar"]

ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","./norris-jokes.jar"]



