FROM ubuntu:latest
MAINTAINER Bruno G. Pinto

RUN useradd -ms /bin/bash jenkins
ARG VERSION=v1.9.1+hotfix.2

#https://storage.googleapis.com/flutter_infra/releases/stable/linux/flutter_linux_v1.9.1+hotfix.2-stable.tar.xz

RUN apt-get update && apt-get install -y curl make git bzip2 xz-utils wget unzip
RUN wget https://storage.googleapis.com/flutter_infra/releases/stable/linux/flutter_linux_v1.9.1+hotfix.2-stable.tar.xz
RUN tar xvf flutter_linux_v1.9.1+hotfix.2-stable.tar.xz
RUN rm flutter_linux_v1.9.1+hotfix.2-stable.tar.xz

ENV PATH $PATH:/flutter/bin/cache/dart-sdk/bin:/flutter/bin

RUN flutter doctor