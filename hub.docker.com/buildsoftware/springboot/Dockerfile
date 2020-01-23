FROM openjdk:8-jdk-alpine

#WORKDIR /var/jenkins_home/workspace/spring-pipeline
#VOLUME /var/jenkins_home/workspace/spring-pipeline

#RUN pwd
#ENV DIRPATH /path
#WORKDIR $DIRPATH/$DIRNAME
#RUN pwd

VOLUME /tmp
#RUN ls -l /target
ARG PROJECT_NAME

COPY /${PROJECT_NAME} contact.jar
ADD /${PROJECT_NAME} contact.jar

ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","contact.jar"]
