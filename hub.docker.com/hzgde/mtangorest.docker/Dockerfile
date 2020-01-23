FROM openjdk:8-jre

MAINTAINER wpi@hzg.de

ENV MTANGOREST_VERSION=rc4-2.9

ENV REST_API_PORT=10001

RUN useradd -ms /bin/bash rest

WORKDIR /home/rest

RUN wget https://github.com/Ingvord/mtangorest.server/releases/download/mtangorest.server-${MTANGOREST_VERSION}/mtangorest.server-${MTANGOREST_VERSION}.jar

EXPOSE ${REST_API_PORT}

ENTRYPOINT java -DTANGO_HOST=${TANGO_HOST} -DTOMCAT_PORT=${REST_API_PORT} -DTANGO_ACCESS=${TANGO_ACCESS} -jar mtangorest.server-${MTANGOREST_VERSION}.jar -nodb -dlist sys/rest/0