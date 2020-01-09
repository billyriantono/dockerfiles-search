FROM openjdk:8-jre-alpine

ENV SBT_VERSION 0.13.15

RUN apk add --no-cache bash curl openrc git && \
    curl -sL "http://dl.bintray.com/sbt/native-packages/sbt/$SBT_VERSION/sbt-$SBT_VERSION.tgz" | gunzip | tar -x -C /usr/local && \
    ln -s /usr/local/sbt/bin/sbt /usr/local/bin/sbt && \
    chmod 0755 /usr/local/bin/sbt && \
    apk add --no-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/main --repository  http://dl-cdn.alpinelinux.org/alpine/edge/community docker

RUN rc-update add docker
ADD build.sbt /tmp
RUN mkdir -p /tmp/project
ADD project/Commons.scala /tmp/project/Commons.scala
ADD project/plugins.sbt /tmp/project/plugins.sbt
ADD project/build.properties /tmp/project/build.properties
WORKDIR /tmp
RUN sbt reload
RUN sbt update
ADD src /tmp/src
ADD runAfterTime.sh /tmp
RUN sbt stage
RUN chmod +x runAfterTime.sh
ENTRYPOINT [ "./runAfterTime.sh" ]