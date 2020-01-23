FROM mdillon/postgis:9.5

MAINTAINER Stefan Kuethe <crazycapivara@gmail.com>

ENV TDS_FWD_VERSION="1.0.7"

RUN apt-get update \
	&& apt-get install -y build-essential wget libsybdb5 freetds-dev freetds-common postgresql-client-9.5 postgresql-server-dev-9.5

RUN wget https://github.com/tds-fdw/tds_fdw/archive/v${TDS_FWD_VERSION}.tar.gz \
	&& tar -xvzf v${TDS_FWD_VERSION}.tar.gz

RUN cd tds_fdw-${TDS_FWD_VERSION} \
	&& make USE_PGXS=1 \
	&& make USE_PGXS=1 install

