FROM openjdk:8u201-jre-alpine

LABEL maintainer "Blackn0va"

RUN apk add --no-cache -U \
  openssl \
  imagemagick \
  lsof \
  su-exec \
  shadow \
  bash \
  curl iputils wget \
  git \
  jq \
  mysql-client \
  tzdata \
  rsync \
  nano \
  python python-dev py2-pip

RUN pip install mcstatus

 
RUN wget -q https://cdn.getbukkit.org/craftbukkit/craftbukkit-1.14.1-R0.1-SNAPSHOT.jar;
 
WORKDIR /data
VOLUME /data

HEALTHCHECK CMD mcstatus localhost:$SERVER_PORT ping

	

EXPOSE 25565 25575

CMD echo eula=true > /data/eula.txt && java -Xmx16384M -Xms16384M -jar /craftbukkit-1.14.1-R0.1-SNAPSHOT.jar nogui
