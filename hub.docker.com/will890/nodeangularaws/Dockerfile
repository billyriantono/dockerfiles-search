FROM node:8.11.4-jessie

RUN apt-get update && \
    apt-get install -y  python python-pip python-dev


RUN echo deb http://http.debian.net/debian jessie-backports main > /etc/apt/sources.list.d/jessie-backports.list && \
    apt-get update && \
    apt-get install -t jessie-backports openjdk-8-jdk -y

CMD ["/usr/bin/java", "-version"]

RUN npm install -g \
    @angular/cli@6.2.1

ENV AWSCLI_VERSION=1.16.10
RUN pip install awscli==1.16.10
