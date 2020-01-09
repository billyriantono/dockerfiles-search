FROM ubuntu:latest

MAINTAINER kramos <markosrendell@gmail.com>


# Install Gradle
RUN apt-get update -y && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:cwchien/gradle -y && \
    apt-get update -y && \
    apt-get install gradle -y

# Install JDK
RUN apt-get install -y default-jdk


CMD gradle --version 

