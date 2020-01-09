FROM openjdk:8
ADD /target/springdocker-demos.jar Ticket.jar
ENTRYPOINT ["java","-Dserver.port=8090", "-jar","app.jar"]
