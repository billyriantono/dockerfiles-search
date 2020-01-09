FROM ubuntu:trusty
MAINTAINER Justin Morris <morris.justin@gmail.com>

RUN apt-get update && apt-get install -y \
    git-core \
    python

RUN git clone https://github.com/RuudBurger/CouchPotatoServer.git /couchpotato

RUN apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/* \
    && rm -rf /var/tmp/*

VOLUME /volumes/config/couchpotato /volumes/data
EXPOSE 5050

CMD [ "/usr/bin/python", "/couchpotato/CouchPotato.py", "--data_dir", "/volumes/data/", "--config_file", "/volumes/config/couchpotato/CouchPotato.cfg", "--console_log" ]
