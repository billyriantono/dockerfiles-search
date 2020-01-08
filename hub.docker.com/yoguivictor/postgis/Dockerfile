FROM		postgres:9.4
MAINTAINER	Victor M. Varela <v.varela@neartechnologies.com>

ENV		POSTGIS_MAJOR 	2.1
ENV		POSTGIS_VERSION	2.1.7+dfsg-0~exp1.pgdg70+1

RUN		echo deb http://http.debian.net/debian wheezy-backports main >> /etc/apt/sources.list
RUN		apt-get update \
	&&	apt-get install -y --no-install-recommends \
			postgresql-$PG_MAJOR-postgis-$POSTGIS_MAJOR=$POSTGIS_VERSION \
			postgis=$POSTGIS_VERSION pgtune \
	&&	rm -rf /var/lib/apt/lists/*

RUN		mkdir -p /docker-entrypoint-initdb.d
COPY		./initdb-postgis.sh	/docker-entrypoint-initdb.d/postgis.sh
COPY		./initdb-config.sh	/docker-entrypoint-initdb.d/config.sh

ENV		POSTGRES_USER			scott
ENV		POSTGRES_PASSWORD		tiger
ENV		POSTGRES_DB			db

ENV		MAX_CONNECTIONS			400
ENV		CHECKPOINT_SEGMENTS		3
ENV		DEFAULT_STATISTICS_TARGET	50
ENV		MAINTENANCE_WORK_MEM		448MB
ENV		CONSTRAINT_EXCLUSION		on
ENV		CHECKPOINT_COMPLETION_TARGET	0.9
ENV		EFFECTIVE_CACHE_SIZE		5632MB
ENV		WORK_MEM			9MB
ENV		WAL_BUFFERS			8MB
ENV		CHECKPOINT_SEGMENTS		16
ENV		SHARED_BUFFERS			1792MB

