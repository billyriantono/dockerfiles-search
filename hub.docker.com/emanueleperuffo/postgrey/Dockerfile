FROM emanueleperuffo/baseimage-debian:latest
MAINTAINER Emanuele Peruffo <info@emanueleperuffo.com>

ENV HOME /root
ADD . /build

ENV POSTGREY_DELAY 300
ENV POSTGREY_MAX_AGE 35
ENV POSTGREY_RETRY_WINDOW 2
ENV POSTGREY_AUTO_WHITELIST_CLIENTS 5

RUN /build/prepare.sh && \
	/build/services.sh && \
	/build/cleanup.sh

EXPOSE 10023

CMD ["/sbin/my_init"]