FROM percona:latest

COPY scripts /usr/local/bin

RUN DEBIAN_FRONTEND=noninteractive apt-get update \
	&& apt-get -y --no-install-recommends install rsync \
												  ssh \
												  pbzip2 \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN echo "show_compatibility_56 = ON" >> /etc/mysql/percona-server.conf.d/mysqld.cnf

RUN chmod +x /usr/local/bin/*

EXPOSE 3306

CMD ["mysqld"]