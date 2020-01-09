FROM phusion/passenger-customizable:0.9.10
MAINTAINER Jon Gillies <supercoder@gmail.com>

# Cloned from git@github.com:timhaak/docker-couchpotato.git, thanks Tim Haak <tim@haak.co.uk>

RUN apt-get -q update
RUN apt-get -qy --force-yes dist-upgrade

RUN apt-get install -qy --force-yes  python git-core
RUN git clone https://github.com/RuudBurger/CouchPotatoServer.git /CouchPotatoServer


VOLUME /config
VOLUME /data

VOLUME /movies
VOLUME /complete

ADD ./start.sh /start.sh
RUN chmod u+x  /start.sh

EXPOSE 5050

RUN apt-get autoremove &&\
    apt-get clean &&\
    rm -rf /var/lib/apt/lists/* &&\
    rm -rf /tmp/*

CMD ["/start.sh"]
