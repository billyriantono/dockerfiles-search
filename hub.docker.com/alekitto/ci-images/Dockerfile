FROM postgres:11

RUN apt-get update && \
    apt-get install --no-install-recommends -y curl ca-certificates make build-essential git-core autoconf automake libtool pkg-config libcurl4-gnutls-dev zlib1g-dev && \
    curl https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - && \
    echo "deb http://apt.postgresql.org/pub/repos/apt/ $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list && \
    apt-get update && \
    apt-get install --no-install-recommends -y postgis postgresql-11-postgis-2.5 postgresql-11-postgis-2.5-scripts postgresql-11-ip4r postgresql-plpython3-11 && \
    apt-get install --no-install-recommends -y postgresql-server-dev-11 && \
    git clone git://sigaev.ru/smlar.git /usr/local/src/smlar && \
    cd /usr/local/src/smlar && \
    make USE_PGXS=1 && make USE_PGXS=1 install && \
    git clone --branch v1.1-alpha https://github.com/openvenues/libpostal.git /usr/local/src/libpostal && \
    cd /usr/local/src/libpostal && \
    ./bootstrap.sh && ./configure && \
    make -j4 && make install && ldconfig && \
    git clone https://github.com/pramsey/pgsql-postal.git /usr/local/src/pgsql-postal && \
    cd /usr/local/src/pgsql-postal && \
    make -j4 && make install && \
    git clone --branch develop https://github.com/zombodb/zombodb.git /usr/local/src/zombodb && \
    cd /usr/local/src/zombodb && \
    make -j4 && make install && \
    apt-get purge -y postgresql-server-dev-11 make build-essential git-core autoconf automake libtool pkg-config && apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/*
