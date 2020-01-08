FROM postgres:10

ENV SCWS_VERSION 1.2.3
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates wget \
    && apt-get install -y tar make gcc
RUN apt-get install -y postgresql-server-dev-$PG_MAJOR
RUN mkdir build \
    && cd build \
    && wget -q -O - http://www.xunsearch.com/scws/down/scws-$SCWS_VERSION.tar.bz2 | tar xjf -  \
    && cd scws-$SCWS_VERSION ; ./configure ; make install ; cd ..
RUN apt-get install -y git
RUN git clone https://github.com/amutu/zhparser.git \
    && cd zhparser \
    && SCWS_HOME=/usr/local make && make install
