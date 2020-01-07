FROM ubuntu

WORKDIR /development

ADD https://storage.googleapis.com/golang/go1.7.4.linux-amd64.tar.gz /opt

RUN apt-get update -y && apt-get install vim -y && tar -C /usr/local -xzf /opt/go1.7.4.linux-amd64.tar.gz

ENV PATH=$PATH:/usr/local/go/bin
