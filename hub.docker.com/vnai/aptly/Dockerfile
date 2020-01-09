FROM debian:stretch
MAINTAINER Mike Purvis

RUN apt-get update && \
apt-get install gpgv1 gnupg1 dpkg-sig -y && \
apt-get clean

# Workaround for the ipv6 gpg issue
RUN mkdir ~/.gnupg && echo "disable-ipv6" >> ~/.gnupg/dirmngr.conf

# Instructions from: http://www.aptly.info/download/
RUN echo "deb http://repo.aptly.info/ squeeze main" > /etc/apt/sources.list.d/aptly.list && \
apt-key adv --keyserver pool.sks-keyservers.net --recv-keys ED75B5A4483DA07C && \
apt-get update && \
apt-get install aptly ca-certificates -y && \
apt-get clean

ADD aptly.conf /etc/aptly.conf
VOLUME ["/aptly"]
