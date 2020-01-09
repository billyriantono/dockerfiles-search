FROM debian:jessie

MAINTAINER Fork from Martin Janser by Philippe Le Van (@plv)

RUN apt-get update && apt-get install -y rubygems git
RUN gem install net-ssh -v 2.9.2
RUN gem install capifony -v 2.8.3

ENV SSH_AUTH_SOCK /root/ssh-agent

WORKDIR /root/workdir

ENTRYPOINT ["cap"]
