FROM bthuillier/openjdk8:latest
MAINTAINER Benjamin Thuillier <benjaminthuillier@gmail.com>

ENV LEIN_ROOT true

RUN wget -q -O /usr/bin/lein \
    https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein \
    && chmod +x /usr/bin/lein

RUN lein
