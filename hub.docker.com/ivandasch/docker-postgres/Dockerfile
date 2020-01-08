FROM postgres:9.4

RUN apt-get update \
	&& apt-get install -y \
			postgresql-server-dev-$PG_MAJOR=$PG_VERSION \
			git \
			build-essential

RUN git clone https://github.com/erthalion/jsonbx.git /src/jsonbx
RUN cd /src/jsonbx && make && make install
ADD create_db.sh docker-entrypoint-initdb.d/create_db.sh

