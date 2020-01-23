FROM sselzer/maven-gitcrypt:3-jdk-11

MAINTAINER Sascha Selzer sascha.selzer@gmail.com

RUN apt-get update && apt-get install -y \
    awscli && \
    rm -rf /var/lib/apt/lists/*