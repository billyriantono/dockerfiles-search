FROM maven:3.5.2-jdk-8-alpine
RUN mkdir /home/userinformation
WORKDIR /home/userinformation
COPY . .
RUN mvn clean install
EXPOSE 8080
CMD ["java", "-jar", "/home/userinformation/target/demo-0.0.1-SNAPSHOT.jar"]