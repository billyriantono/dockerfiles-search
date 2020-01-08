FROM ubuntu:xenial
# following this tutorial: https://www.torproject.org/docs/debian.html.en#ubuntu

RUN echo 'deb http://deb.torproject.org/torproject.org xenial main' > /etc/apt/sources.list.d/tor.list
RUN echo 'deb-src http://deb.torproject.org/torproject.org xenial main' >> /etc/apt/sources.list.d/tor.list

RUN gpg --keyserver keys.gnupg.net --recv A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89
RUN gpg --export A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89 | apt-key add -

RUN apt-get update
RUN apt-get -y install tor deb.torproject.org-keyring

# setup the tor user
ENV HOME=/home/tor
RUN useradd -m -d $HOME tor
USER tor
ENV USER=tor
WORKDIR $HOME

ENTRYPOINT ./start-tor.sh

ADD start-tor.sh start-tor.sh
ADD create-tor-config-from-environment-variables.sh \
    create-tor-config-from-environment-variables.sh
