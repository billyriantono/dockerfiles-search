FROM openjdk:8 AS build

ARG PAPER_VERSION=1.14
ARG PAPER_BUILD_NUMBER=127

RUN wget -O paperclip.jar -c https://papermc.io/ci/job/Paper-${PAPER_VERSION}/${PAPER_BUILD_NUMBER}/artifact/paperclip-${PAPER_BUILD_NUMBER}.jar && \
    java -jar paperclip.jar

RUN mv cache/patched*.jar paper.jar

FROM anapsix/alpine-java:latest

ARG PAPER_HOME=/paper

ENV JAVA_ARGS "-Xmx2G"

WORKDIR ${PAPER_HOME}

VOLUME ${PAPER_HOME}

COPY --from=build paper.jar /paper.jar

EXPOSE 25565

ENTRYPOINT ["java", "-jar", "/paper.jar"]
