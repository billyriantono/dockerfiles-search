FROM ubuntu:latest
MAINTAINER jusrob <jrob48@gmail.com>

ENV LANG en_US.UTF-8
RUN locale-gen $LANG

RUN apt-get update -q  && \
    apt-get install git python -qy && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /var/tmp/*

RUN git clone https://github.com/drzoidberg33/plexpy.git /opt/plexpy

VOLUME ["/data"]
EXPOSE 8181

CMD ["/usr/bin/python", "/opt/plexpy/PlexPy.py", "--datadir=/data"]
