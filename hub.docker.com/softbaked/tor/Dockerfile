FROM ubuntu:14.04

RUN echo deb http://deb.torproject.org/torproject.org trusty main > /etc/apt/sources.list.d/tor.list

RUN gpg --keyserver keys.gnupg.net --recv 886DDD89
RUN gpg --export A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89 | sudo apt-key add -

RUN apt-get update
RUN apt-get install -y tor deb.torproject.org-keyring

RUN apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD torrc /etc/tor/torrc

EXPOSE 9050
CMD ["/usr/sbin/tor"]
