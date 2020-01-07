FROM golang:latest
MAINTAINER Oscar

RUN wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | apt-key add -
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ jessie-pgdg main" >> /etc/apt/sources.list.d/pgdg.list

RUN \
	apt-get update; \
	apt-get install -y postgresql postgresql-contrib; \
	rm /etc/postgresql/9.6/main/pg_hba.conf; \
	echo 'local   all             all                                     trust' >> /etc/postgresql/9.6/main/pg_hba.conf; \
	echo 'host    all             all             127.0.0.1/8             trust' >> /etc/postgresql/9.6/main/pg_hba.conf; \
	echo 'host    all             all             ::1/128                 trust' >> /etc/postgresql/9.6/main/pg_hba.conf; \
	echo 'host    all             all             ::0/0                   trust' >> /etc/postgresql/9.6/main/pg_hba.conf; \
	apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*