FROM debian:jessie-slim

LABEL maintainer="f@f213.in"


RUN apt-get update && \
        apt-get --no-install-recommends install -y build-essential postgresql-server-dev-all libxml2-dev libxslt1-dev && \
        apt-get --no-install-recommends install -y libjpeg62-turbo-dev libopenjpeg-dev libfreetype6-dev libtiff5-dev liblcms2-dev libwebp-dev tk8.6-dev && \
        apt-get --no-install-recommends install -y libffi-dev libcgraph6 libgraphviz-dev libzmq-dev && \
        apt-get --no-install-recommends install -y python2.7 python2.7-dev python-pip supervisor