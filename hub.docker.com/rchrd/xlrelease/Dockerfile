FROM java:8-jre-alpine

RUN apk add --no-cache curl openssl jq

ENV version 6.2.0
ENV root /lib
ENV home ${root}/xl-release-server

RUN wget -q \
      https://dist.xebialabs.com/public/trial/xl-release/xl-release-${version}-server.zip \
      -O /tmp/xlr-server.zip \
    && unzip \
      /tmp/xlr-server.zip \
      -d ${root} \
    && mv \
      ${root}/xl-release-${version}-server \
      ${root}/xl-release-server \
    && rm -R \
      /tmp/xlr-server.zip \
      ${home}/serviceWrapper

ADD xlrelease.answers ${home}/bin/xlrelease.answers

WORKDIR ${home}/bin

RUN ["./run.sh", "-setup", "-reinitialize", "-force", "-setup-defaults", "./bin/xlrelease.answers"]

EXPOSE 5516

CMD ["./run.sh"]
