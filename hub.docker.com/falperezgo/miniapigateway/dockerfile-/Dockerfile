FROM ubuntu:trusty
MAINTAINER Justin Morris <morris.justin@gmail.com>

RUN echo "deb http://archive.ubuntu.com/ubuntu trusty multiverse" >> /etc/apt/sources.list \
    && echo "deb http://ppa.launchpad.net/jcfp/ppa/ubuntu $(lsb_release -c -s) main" | sudo tee -a /etc/apt/sources.list \
    && sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:11371 --recv-keys 0x98703123E0F52B2BE16D586EF13930B14BB9F05F

RUN apt-get update && apt-get install -y \
    sabnzbdplus \
    sabnzbdplus-theme-classic \
    sabnzbdplus-theme-mobile \
    sabnzbdplus-theme-plush \
    par2 \
    python-yenc \
    unzip \
    unrar

RUN apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/* \
    && rm -rf /var/tmp/*

VOLUME /config /downloads

EXPOSE 8080 9090

CMD [ "/usr/bin/sabnzbdplus", "--config-file", "/config", "--server", "0.0.0.0:8080" ]
