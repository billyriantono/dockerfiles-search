FROM debian:jessie
ENV DEBIAN_FRONTEND noninteractive

# Install dependencies
RUN apt-get -qq update
RUN apt-get --no-install-recommends -y install \
    build-essential pkg-config erlang \
    libicu-dev libmozjs185-dev libcurl4-openssl-dev \
    wget

# Download CouchDB source
WORKDIR /
RUN wget -nv http://apache.mirrors.spacedump.net/couchdb/source/2.0.0/apache-couchdb-2.0.0.tar.gz \
 && tar -xf apache-couchdb-2.0.0.tar.gz \  
 && rm apache-couchdb-2.0.0.tar.gz 

# Build CouchDB into /couchdb
WORKDIR /apache-couchdb-2.0.0
RUN ./configure && make release \
 && cp -r rel/couchdb /couchdb \
 && cd / \
 && rm -rf /apache-couchdb-2.0.0

# Setup CouchDB permissions and defaults
WORKDIR /couchdb
RUN sed -i'' 's/bind_address = 127.0.0.1/bind_address = 0.0.0.0/' etc/default.ini

EXPOSE 5984
ENTRYPOINT ["/couchdb/bin/couchdb"]
