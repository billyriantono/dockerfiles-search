FROM asterios/mysql:master

# InnoDb
# innodb_flush_method	= O_DIRECT (unable on tmpfs)
RUN echo [mysqld] > /etc/mysql/conf.d/innodb.cnf \
	&& echo innodb_file_per_table	= 1 >> /etc/mysql/conf.d/innodb.cnf \
	&& echo default-storage-engine	= myisam >> /etc/mysql/conf.d/innodb.cnf