FROM ubuntu:14.04
MAINTAINER James Turnbull <james@example.com>
ENV REFRESHED_AT 2014-06-01

RUN apt-get -qq update
RUN apt-get -qqy install ruby make ruby-dev curl

RUN gem install --no-rdoc --no-ri tprov

RUN curl https://get.docker.io/builds/Linux/x86_64/docker-latest -o /usr/local/bin/docker
RUN chmod +x /usr/local/bin/docker

VOLUME [ "/docker.sock"]

EXPOSE 4567

ENV DOCKER_HOST unix:///docker.sock

ENTRYPOINT [ "/usr/local/bin/tprov"]