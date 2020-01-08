FROM java:openjdk-8-jdk
VOLUME /tmp
ADD ./target/SimpleWarehouseApp-0.1.0.jar app.jar
RUN bash -c 'touch /app.jar'
EXPOSE 8080

ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]