FROM ubuntu:14.04

MAINTAINER Christoph Castor "christoph@castor.io"
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update
RUN rm /etc/apt/apt.conf.d/docker-gzip-indexes
RUN apt-get purge apt-show-versions
RUN apt-get -o Acquire::GzipIndexes=false update
RUN apt-get install -yq apt-show-versions
RUN apt-get install -yq  wget nginx fail2ban gnupg
RUN wget http://repo.ajenti.org/debian/key -O- | apt-key add -
RUN echo "deb http://repo.ajenti.org/ng/debian main main ubuntu" | tee -a /etc/apt/sources.list
RUN echo "deb http://ppa.launchpad.net/certbot/certbot/ubuntu trusty main" | tee -a /etc/apt/sources.list
RUN echo "deb-src http://ppa.launchpad.net/certbot/certbot/ubuntu trusty main" | tee -a /etc/apt/sources.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 7BF576066ADA65728FC7E70A8C47BE8E75BCA694
RUN apt-get update
RUN apt-get install -yq ajenti
RUN service ajenti restart
RUN apt-get install -yq python-certbot-nginx
ENV DEBIAN_FRONTEND teletype
CMD service ajenti restart && service nginx restart && tail -f /dev/null