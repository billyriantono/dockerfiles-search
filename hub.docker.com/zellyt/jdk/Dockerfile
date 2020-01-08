FROM openjdk:11.0.2-jdk-stretch
LABEL maintainer="Zellyt IT <it@zellyt.com>"

COPY files/gradle/gradle-5.3-bin.zip opt/gradle/

# Adding required packages
RUN apt-get update && apt-get install -y zip

WORKDIR /opt/gradle

RUN unzip gradle-5.3-bin.zip \
    && rm gradle-5.3-bin.zip

RUN printf "\n"'export PATH=$PATH:/opt/gradle/gradle-5.3/bin'"\n" >> ~/.bashrc

WORKDIR /usr/src/app
