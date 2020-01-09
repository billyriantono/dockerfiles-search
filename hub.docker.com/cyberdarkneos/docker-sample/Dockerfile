FROM maven:3.3.3-jdk-8-onbuild

ADD . usr/local/docker-sample

RUN cd usr/local/docker-sample && mvn install 

EXPOSE 9237

CMD ["java", "-cp", "usr/local/docker-sample/target/server-test-1.0-SNAPSHOT.jar", "com.amplience.docker.sample.server.Main" ]
