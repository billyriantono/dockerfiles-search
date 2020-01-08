FROM openjdk:11.0.1-jre-stretch

RUN apt-get update && \
yes | apt-get install git curl && \
curl -fsSL get.docker.com -o get-docker.sh && \
sh get-docker.sh
