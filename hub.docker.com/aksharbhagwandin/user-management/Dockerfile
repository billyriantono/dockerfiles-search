FROM maven:alpine
LABEL maintainer="akshar@zailab.com"
ADD src /src
ADD pom.xml /pom.xml
RUN mvn clean package
VOLUME /tmp
EXPOSE 8080
ENTRYPOINT ["java","-jar","/target/userView-management.jar"]

