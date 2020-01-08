FROM alpine/git as clone
WORKDIR /app
ARG auth
ARG branch=master
RUN git clone https://40f22606ed734ffddb6d58457e078ac32434c48d@github.com/SouthbankSoftware/provendb-tree.git --branch=${branch}

FROM golang:latest as build
ENV GOPATH /app/go
ENV PATH="/app/go/bin:${PATH}"
ENV GO111MODULE=on
WORKDIR /app/go/src
COPY --from=clone /app/provendb-tree /app/go/src/github.com/SouthbankSoftware/provendb-tree
WORKDIR /app/go/src/github.com/SouthbankSoftware/provendb-tree
ENV GOOS linux
ENV GOARCH amd64

FROM node:8-jessie
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4 \
  && echo "deb http://repo.mongodb.org/apt/debian jessie/mongodb-org/4.0 main" | tee /etc/apt/sources.list.d/mongodb-org-4.0.list \
  && apt-get update \
  && apt-get install -y mongodb-org-shell=4.0.0 mongodb-org-tools=4.0.0 \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*dock

RUN apt-get update -y && \
    apt-get install python-pip -y

WORKDIR /usr/lib/jvm
RUN wget https://download.java.net/java/GA/jdk11/9/GPL/openjdk-11.0.2_linux-x64_bin.tar.gz
RUN tar -xvzf openjdk-11.0.2_linux-x64_bin.tar.gz
ENV JAVA_HOME='/usr/lib/jvm/jdk-11.0.2' 
ENV PATH=$PATH:$HOME/bin:$JAVA_HOME/bin
WORKDIR /opt
RUN wget http://apache.mirror.serversaustralia.com.au/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.tar.gz
RUN tar -xvzf apache-maven-3.6.0-bin.tar.gz
ENV M2_HOME='/opt/apache-maven-3.6.0'
ENV PATH=$PATH:$M2_HOME/bin

WORKDIR /opt
RUN wget https://dl.google.com/go/go1.12.1.linux-amd64.tar.gz
RUN tar -C /usr/local -xzf go1.12.1.linux-amd64.tar.gz
ENV PATH=$PATH:/usr/local/go/bin
RUN go version