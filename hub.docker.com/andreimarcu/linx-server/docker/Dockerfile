FROM blang/latex

MAINTAINER Baudouin Feildel <baudouin@feildel.fr>

RUN apt-get -yqq update && apt-get -yqq upgrade
RUN apt-get -yqq install biber xindy

RUN apt-get autoclean
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /data
VOLUME ["/data"]
