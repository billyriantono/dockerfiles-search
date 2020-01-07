FROM postgres:9.6.11

ENV SCWS_VERSION 1.2.3
ENV ZHPARSER_VERSION 0.2.0

RUN apt-get update -y && \
	apt-get install -y wget tar make ca-certificates gcc postgresql-server-dev-$PG_MAJOR && \
	rm -rf /var/lib/apt/lists/*

RUN wget -q -O - http://www.xunsearch.com/scws/down/scws-$SCWS_VERSION.tar.bz2 | tar xjf - && \
	cd scws-$SCWS_VERSION ; ./configure ; make install; cd ..; rm -rf scws-$SCWS_VERSION && \
	wget -q -O - https://github.com/amutu/zhparser/archive/v$ZHPARSER_VERSION.tar.gz | tar xzf - && \
	cd zhparser-$ZHPARSER_VERSION ; SCWS_HOME=/usr/local make && make install && cd .. && rm -rf zhparser-$ZHPARSER_VERSION

RUN echo "CREATE EXTENSION zhparser; \n \
CREATE TEXT SEARCH CONFIGURATION chinese (PARSER = zhparser); \n \
ALTER TEXT SEARCH CONFIGURATION chinese ADD MAPPING FOR n,v,a,i,e,l WITH simple;" > /docker-entrypoint-initdb.d/init-zhparser.sql

