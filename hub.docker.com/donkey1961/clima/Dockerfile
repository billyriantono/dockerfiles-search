FROM maven:3.5.4-jdk-8-alpine

COPY . /app/

RUN ls -R /app && cd /app && mvn clean package
RUN rm -rf /app/src && rm /app/pom.xml 

ENTRYPOINT ["java","-jar", "/app/target/clima-service-0.0.1-SNAPSHOT.jar" ]