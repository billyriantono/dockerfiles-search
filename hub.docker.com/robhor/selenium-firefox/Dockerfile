FROM java:latest

WORKDIR /root

RUN apt-get update -qq && \
    apt-get install -y -qq \
    wget bzip2 x11vnc xvfb libav-tools tcpdump && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN wget -q -O firefox.tar.bz2 http://ftp.mozilla.org/pub/firefox/releases/31.0/linux-x86_64/en-US/firefox-31.0.tar.bz2
RUN wget -q -O selenium-server-standalone.jar http://selenium-release.storage.googleapis.com/2.47/selenium-server-standalone-2.47.1.jar

RUN tar jxf firefox.tar.bz2
RUN ln -s $(pwd)/firefox/firefox /usr/bin/firefox

ADD . .
ENTRYPOINT ["bash", "entrypoint.sh"]

EXPOSE 4444 5900
