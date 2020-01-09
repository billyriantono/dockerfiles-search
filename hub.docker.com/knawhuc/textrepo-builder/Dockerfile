FROM maven:3.6-jdk-11
WORKDIR /build/

COPY ./textrepo-app/pom.xml /build/textrepo-app/
COPY ./concordion/pom.xml /build/concordion/

RUN mvn -f ./textrepo-app/pom.xml de.qaware.maven:go-offline-maven-plugin:resolve-dependencies
RUN mvn -f ./concordion/pom.xml de.qaware.maven:go-offline-maven-plugin:resolve-dependencies
