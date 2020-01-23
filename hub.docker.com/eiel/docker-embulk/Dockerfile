FROM  openjdk:jdk-alpine
MAINTAINER Tomohiko Himura "eiel.hal@gmail.com"

ENV EMBULK_VERSION 0.8.17
RUN apk --update add pcre-dev openssl-dev \
  && apk add --virtual curl \
  && mkdir /embulk \
  && curl -SL -o /embulk/embulk.jar https://bintray.com/artifact/download/embulk/maven/embulk-${EMBULK_VERSION}.jar \
  && apk del curl

WORKDIR /work
ENTRYPOINT ["java", "-jar", "/embulk/embulk.jar"]
CMD ["--help"]
