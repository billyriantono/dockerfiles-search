FROM dockerfile/ubuntu

MAINTAINER Sam Halicke <sam@twenty20.com>

RUN DEBIAN_FRONTEND=noninteractive apt-get -qq update
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install memcached

EXPOSE 11211

CMD /usr/bin/memcached -l 0.0.0.0 -u root
