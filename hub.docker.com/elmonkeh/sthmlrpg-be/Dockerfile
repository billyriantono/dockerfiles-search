FROM maven:3.5-jdk-8 as BUILD

COPY src /usr/src/sthmlrpg/src
COPY pom.xml /usr/src/sthmlrpg
RUN mvn -f /usr/src/sthmlrpg/pom.xml clean package -DskipTests

FROM openjdk:8-jdk-alpine
COPY --from=BUILD /usr/src/sthmlrpg/target/*.jar sthmlrpg.jar
ENTRYPOINT ["java","-jar","/sthmlrpg.jar"]
