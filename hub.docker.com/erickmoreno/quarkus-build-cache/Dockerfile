#Build Environment
FROM quay.io/quarkus/centos-quarkus-maven:19.2.1
USER root

ADD ./pom.xml /project/pom.xml
RUN mvn -B -e -C -T 1C dependency:go-offline
