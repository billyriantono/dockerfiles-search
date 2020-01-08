##############################
########## BUILD-FE ##########
##############################
FROM node:12.2.0 AS buildfe
MAINTAINER starforge
USER root

# install chrome for protractor tests
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
RUN apt-get update && apt-get install -yq google-chrome-stable

# set working directory
WORKDIR /app

# add `/app/node_modules/.bin` to $PATH
ENV PATH /app/node_modules/.bin:$PATH

# install and cache app dependencies
COPY angularclient /app
RUN npm install

# run tests
#RUN ng test --watch=false
#RUN ng e2e --port 4202

# generate build
RUN ng build --output-path=dist


##############################
########## BUILD-BE ##########
##############################
FROM maven:3.5.2-jdk-8-alpine AS buildbe
MAINTAINER starforge
USER root

# set working directory
WORKDIR /app

##### Build BE #####
COPY src /app/src
COPY pom.xml /app
RUN mvn test package


##########################
########## PROD ##########
##########################
FROM node:11-alpine
MAINTAINER starforge
USER root

# inatall openjdk8-jre
RUN apk update
RUN apk fetch openjdk8-jre
RUN apk add openjdk8-jre

# set working directory
WORKDIR /app

# install web server
RUN npm install express express-http-proxy
COPY express-srv.js .

# copy artifact build from the 'build environment'
COPY --from="buildfe" /app/dist /app
COPY --from="buildbe" /app/target/*.jar /app/kafka-test-tool.jar
COPY run.sh /app
COPY src/main/resources/application.properties /app/application.properties.example
COPY src/main/resources/log4j2-spring.xml /app/log4j2-spring.xml

# check results
RUN ls -lah /app

# expose port 80
EXPOSE 80

# run FE and BE
ENTRYPOINT ["sh", "run.sh" ]


# DEBUG
#RUN apk add bash
#RUN apk add mc
#RUN apk add httpie
#ENTRYPOINT ["ping", "localhost" ]
