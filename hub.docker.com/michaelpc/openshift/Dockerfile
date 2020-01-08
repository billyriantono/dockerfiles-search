FROM michaelpc/openshift:latest

USER 0

RUN mkdir /tmp/setup

WORKDIR /tmp/setup

RUN curl http://uwsgi.it/install | bash -s psgi /tmp/setup/uwsgi; \
    chmod -v +x uwsgi; \
    cp -v uwsgi /usr/local/bin

RUN apt-get install -y sqlite3

WORKDIR /app

RUN rm -fr /tmp/setup

USER 1000
