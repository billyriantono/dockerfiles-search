FROM centos

WORKDIR /tmp

RUN ["yum", "install", "-y", "java", "maven"]

ADD pom.xml /tmp/pom.xml
ADD src /tmp/src

RUN ["mvn", "clean", "package"]

RUN ["ls", "/tmp/target"]
RUN ["mkdir", "-p", "/data/logs"]
RUN ["cp", "/tmp/target/spring-boot-docker-demo.jar", "/data"]

EXPOSE 8088

ENTRYPOINT [ "java", "-jar", "/data/spring-boot-docker-demo.jar" ]