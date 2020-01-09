# Dockerfile for rundeck

FROM debian:jessie

MAINTAINER Rémi Jouannet "remijouannet@gmail.com"

#ENV http_proxy http://127.0.0.1:8080/
#ENV https_proxy http://127.0.0.1:8080/

RUN ping -c2 ftp.debian.org
RUN apt-get update
RUN apt-get install -y bash ca-certificates openjdk-7-jre-headless
RUN apt-get install -y bash openssh-client pwgen curl git mysql-client

ADD http://dl.bintray.com/rundeck/rundeck-deb/rundeck-2.6.2-1-GA.deb /tmp/rundeck.deb
COPY . /app
WORKDIR /app
RUN useradd -d /var/lib/rundeck -s /bin/false rundeck
RUN chmod u+x ./run.sh

EXPOSE 4443

CMD ./run.sh
