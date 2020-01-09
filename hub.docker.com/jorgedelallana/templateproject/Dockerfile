FROM java:8

MAINTAINER architecture@datiobd.com

ENV API_HTTP_PORT ${API_HTTP_PORT:-7575}

#Install and update functionality
RUN apt-get update
RUN apt-get install wget

#Download microservice
RUN wget http://nexus.datiobd.com:9081/nexus/service/local/repositories/architecture/content/com/datio/architecture/input-api/1.0/input-api-1.0-bin.tar.gz && tar -xvf input-api-1.0-bin.tar.gz

EXPOSE ${API_HTTP_PORT}

#Execute microservice
WORKDIR /input-api-1.0-SNAPSHOT/bin/
ENTRYPOINT ./App
