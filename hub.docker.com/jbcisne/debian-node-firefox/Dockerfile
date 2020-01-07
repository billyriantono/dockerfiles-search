FROM node:10
LABEL name="node10-firefox"
LABEL maintainer="Juliano Buzanello <jbcisne@gmail.com>"

RUN set -x \
    && apt-get update \
    && apt-get install -y libgtk-3-0 libdbus-glib-1-2

RUN wget https://ftp.mozilla.org/pub/firefox/releases/62.0/linux-x86_64/en-US/firefox-62.0.tar.bz2
RUN tar -xjf firefox-62.0.tar.bz2
RUN mv firefox /opt/firefox62
RUN ln -s /opt/firefox62/firefox-bin /usr/bin/firefox

RUN set -x \
    && node -v \
    && npm -v \