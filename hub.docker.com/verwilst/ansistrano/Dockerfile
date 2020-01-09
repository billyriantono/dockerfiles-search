FROM python

MAINTAINER Bart Verwilst <bart@verwilst.be>

RUN pip install ansible \
    && ansible-galaxy install carlosbuenosvinos.ansistrano-deploy \
    && apt-get update \
    && apt-get -y --no-install-recommends install rsync git \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/* 

