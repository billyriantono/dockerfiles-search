FROM ubuntu:18.04
ENV LC_ALL en_US.UTF-8
ENV DEBIAN_FRONTEND noninteractive
ENV PYTHONIOENCODING utf-8
RUN apt-get update && \
    apt-get install -y postgresql postgresql-contrib sudo \
        postgresql-common libpq-dev python-dev \
        libffi-dev libxml2-dev libxslt1-dev libcairo2 libpango1.0-0 \
        libgdk-pixbuf2.0-0 postgresql-client-10 make g++ git \
        libgraphicsmagick1-dev imagemagick libmagick++-dev \
        libgirepository1.0-dev python-cairo-dev postgresql-server-dev-10 \
        postgresql-10 redis-server python-pip language-pack-en nginx curl \
        software-properties-common && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get install -y nodejs
ADD requirements /requirements
RUN pip install -r /requirements/docker.txt && \
    rm -rf /root/.cache/pip
ADD frontend /frontend
RUN cd /frontend && npm install
