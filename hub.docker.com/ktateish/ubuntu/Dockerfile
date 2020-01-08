FROM ubuntu:trusty
MAINTAINER Katsuyuki Tateishi <kt@wheel.jp>

RUN apt-get update && \
    apt-get install -y \
    	openssh-server \
    	openssh-client \
    	netcat \
	curl \
	vim \
	man-db \
	dnsutils \
	gcc \
	g++ \
	make \
	automake \
	autoconf \
	libtool \
	pkg-config \
    && apt-get clean

ADD docker-entry.sh /

CMD ["/docker-entry.sh"]
