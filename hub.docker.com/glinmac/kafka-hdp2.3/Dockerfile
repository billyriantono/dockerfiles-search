FROM glinmac/centos-java8:latest

MAINTAINER Guillaume Gardey "glinmac@gmail.com"

ENV HDP_VERSION 2.3.2.0
ENV HDP_REPO_URL http://public-repo-1.hortonworks.com/HDP/centos6/2.x/updates/$HDP_VERSION/hdp.repo

RUN \
	curl --output /etc/yum.repos.d/hdp.repo $HDP_REPO_URL && \
	yum install -y zookeeper kafka

ADD start-services.sh /usr/bin/start-services

CMD ["start-services"]

EXPOSE 2181 9092
