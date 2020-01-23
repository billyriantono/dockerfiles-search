FROM debian

RUN \
    apt-get -y -q update \
    && apt-get -y install unoconv \
    && apt-get -y -q clean

#COPY entrypoint.sh /entrypoint.sh

#RUN \
#    chmod +x /entrypoint.sh

MAINTAINER  Andreas Kasper <andreas.kasper@goo1.de>

CMD         ["-h"]
ENTRYPOINT  ["unoconv"]
