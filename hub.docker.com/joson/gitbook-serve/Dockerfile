FROM node:latest

MAINTAINER joson chen <josonchen@sina.com>

LABEL version="2.6.7"

RUN npm install -g gitbook-cli  && \
	apt-get clean autoclean && npm cache clear && \
	rm -rf /tmp/* /var/lib/{apt,dpkg,cache,log}/*

# RUN  mkdir /gitbook
# Ubuntu had create the dir /srv,create the dir /srv/gitbook on install gitbook
WORKDIR /srv/gitbook
VOLUME /srv/gitbook /srv/html

EXPOSE 4000 35729

CMD  /usr/local/bin/gitbook,serve
#CMD  /usr/local/bin/gitbook,serve,/gitbook
