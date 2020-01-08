# VERSION   0.1

FROM ubuntu:14.04
MAINTAINER Mark Mims <mark@svds.com>

RUN apt-get update # updated_at 2015-10-22
RUN apt-get -qq install -y curl python
RUN localedef -i en_US -f UTF-8 en_US.UTF-8

#RUN curl -s http://archive.cloudera.com/cdh5/ubuntu/trusty/amd64/cdh/archive.key | apt-key add -
#ADD cm.list /etc/apt/sources.list.d/cm.list
#RUN apt-get update # updated_at 2015-10-22

ADD install-cm-agent.sh /usr/local/sbin/install-cm-agent.sh
CMD ["/usr/local/sbin/install-cm-agent.sh"]
