FROM maven:3.6.1-jdk-11-slim AS buildenv  

RUN mkdir -p /usr/src/app 
WORKDIR /usr/src/app  

ONBUILD ADD pom.xml /usr/src/app
ONBUILD RUN mvn dependency:go-offline

ONBUILD ADD . /usr/src/app  
ONBUILD RUN mvn install
