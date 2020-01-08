FROM openjdk:11-jdk
LABEL maintainer="Perrit B.V. <support@perrit.nl>"
RUN apt-get update \
 && apt install ant -y \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
