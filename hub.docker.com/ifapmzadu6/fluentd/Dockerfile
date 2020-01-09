FROM ubuntu:latest

EXPOSE 8888 80

RUN apt-get install -y curl git

RUN curl -L http://toolbelt.treasuredata.com/sh/install-ubuntu-trusty-td-agent2.sh | sh
ADD Resource/td-agnet.conf /etc/td-agent/td-agnet.conf
RUN /etc/init.d/td-agent start
RUN tail -f /var/log/td-agent/td-agent.log


