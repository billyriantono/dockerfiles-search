FROM maven:3.5.4-jdk-8-alpine AS build

RUN apk add --update --no-cache \
    git

RUN mkdir /app
WORKDIR /app
RUN git clone https://github.com/plantuml/plantuml-server.git -b master --depth 1

WORKDIR /app/plantuml-server
RUN git checkout -b build v1.2018.12
ENV MAVEN_CONFIG=.m2
RUN mvn package

FROM jetty:9.4.12-jre8-alpine

USER root

RUN apk add --update --no-cache \
    curl \
    fontconfig \
    graphviz
COPY local.conf /etc/fonts/
RUN true \
  && mkdir /fonts \
  && mkdir -p /usr/share/fonts/noto \
  && curl -o /fonts/sans.ja.zip https://noto-website-2.storage.googleapis.com/pkgs/NotoSansCJKjp-hinted.zip \
  && curl -o /fonts/serif.ja.zip https://noto-website-2.storage.googleapis.com/pkgs/NotoSerifCJKjp-hinted.zip \
  && unzip '/fonts/sans.ja.zip' -o -d /fonts \
  && unzip '/fonts/serif.ja.zip' -o -d /fonts \
  && cp /fonts/*.otf /usr/share/fonts/noto && chmod 755 /usr/share/fonts/noto/*.otf \
  && fc-cache -f \
  && rm -rf /fonts

RUN mkdir /app
COPY --from=build /app/plantuml-server/target/plantuml.war /app/
COPY --from=build /app/plantuml-server/target/dependency/jetty-runner.jar /app/

USER jetty

WORKDIR /app
ENV HOME /app
EXPOSE 8080
CMD java -Djetty.contextpath=/ -jar jetty-runner.jar plantuml.war
