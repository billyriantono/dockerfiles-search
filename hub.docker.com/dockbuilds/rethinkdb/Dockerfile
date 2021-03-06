FROM ubuntu:14.04

ENV RETHINKDB_VERSION 1.15.0-1-0ubuntu1~trusty

# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN groupadd -r rethinkdb && useradd -r -g rethinkdb rethinkdb

RUN echo "deb http://download.rethinkdb.com/apt trusty main" | tee /etc/apt/sources.list.d/rethinkdb.list
ADD http://download.rethinkdb.com/apt/pubkey.gpg /pubkey.gpg
RUN apt-key add pubkey.gpg

RUN apt-get update && apt-get install -y \
  curl \
  rethinkdb=$RETHINKDB_VERSION \
  && rm -rf /var/lib/apt/lists/*

RUN curl -o /usr/local/bin/gosu -SL 'https://github.com/tianon/gosu/releases/download/1.1/gosu' \
  && chmod +x /usr/local/bin/gosu \
  && apt-get purge -y curl \
  && apt-get autoremove -y

VOLUME /data
WORKDIR /data

ADD ./docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE 8080 28015 29015

CMD ["rethinkdb", "--bind", "all", "-d", "/data"]