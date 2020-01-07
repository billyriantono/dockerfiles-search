FROM maven:3.5-jdk-8 AS build  
COPY src /usr/src/app/src  
COPY pom.xml /usr/src/app  
RUN mvn -f /usr/src/app/pom.xml clean install -DskipTests

FROM openjdk:8-jdk
COPY --from=build /root/.m2/repository/com/nagarro/nagp/cloud-assignment/0.0.1-SNAPSHOT/cloud-assignment-0.0.1-SNAPSHOT.jar /usr/app/cloud-assignment-0.0.1-SNAPSHOT.jar  
EXPOSE 8080  
ENTRYPOINT ["java","-jar","/usr/app/cloud-assignment-0.0.1-SNAPSHOT.jar"]  



