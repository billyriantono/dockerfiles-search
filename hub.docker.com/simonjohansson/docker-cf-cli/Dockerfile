FROM debian
MAINTAINER Simon Johansson <simon@simonjohansson.com>

VOLUME ["/data"]
WORKDIR ["/data"]

RUN apt-get update && apt-get -y install wget ca-certificates

RUN wget -O - "http://cli.run.pivotal.io/stable?release=linux64-binary&source=github" | tar -C /usr/local/bin -zxf -
