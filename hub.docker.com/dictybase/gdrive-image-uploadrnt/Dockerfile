FROM java:8-alpine
ADD stresser.jar /stresser.jar
RUN chmod 755 /stresser.jar
ENTRYPOINT ["java", "-jar", "/stresser.jar"]
