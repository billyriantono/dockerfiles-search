FROM maven:3.5-jdk-8 AS build
COPY src /usr/employeeService/src
COPY pom.xml /usr/employeeService
RUN mvn -f /usr/employeeService/pom.xml clean package
EXPOSE 8080
ENTRYPOINT ["java","-Dspring.data.mongodb.uri=mongodb://mymongodb:27017/glarimy","-jar","/usr/employeeService/target/quiz-employee-service-1.0.0.jar"]