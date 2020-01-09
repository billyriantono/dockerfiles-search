FROM maven:3.3.3-jdk-8

EXPOSE 8080

ADD . /src/myapp

RUN cd /src/myapp && mvn package
WORKDIR /src/myapp/target

CMD ["java", "-jar", "hellospringbootdocker-1.0-SNAPSHOT.jar"]

