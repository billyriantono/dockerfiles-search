FROM ubuntu:14.04
MAINTAINER guihatano

ENV MYSQL_VERSION 5.6

# Just to avoid "debconf: unable to initialize frontend: Dialog" 
ENV DEBIAN_FRONTEND noninteractive

# The "/var/lib/mysql" stuff here is because the mysql-server postinst doesn't have an explicit way to disable 
# the mysql_install_db codepath besides having a database already "configured" (ie, stuff in /var/lib/mysql/mysql)
RUN apt-get update \
	&& apt-get install -y mysql-server-${MYSQL_VERSION} \
	&& rm -rf /var/lib/apt/lists/* \
	&& rm -rf /var/lib/mysql && mkdir -p /var/lib/mysql

# comment out a few problematic configuration values
RUN sed -Ei 's/^(bind-address|log)/#&/' /etc/mysql/my.cnf

# replaces deprecated options
RUN sed -Ei 's/key_buffer/key_buffer_size/' /etc/mysql/my.cnf \
        && sed -Ei 's/myisam-recover/myisam-recover-options/' /etc/mysql/my.cnf

VOLUME /var/lib/mysql

COPY docker-entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

EXPOSE 3306
CMD ["mysqld", "--explicit_defaults_for_timestamp=TRUE"]
