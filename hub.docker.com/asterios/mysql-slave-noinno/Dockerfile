FROM asterios/mysql-slave

RUN echo [mysqld] > /etc/mysql/conf.d/noinnodb.cnf \
	&& echo innodb=OFF >> /etc/mysql/conf.d/noinnodb.cnf \
	&& echo ignore-builtin-innodb >> /etc/mysql/conf.d/noinnodb.cnf \
	&& echo default-storage-engine = myisam >> /etc/mysql/conf.d/noinnodb.cnf \
	&& echo default-tmp-storage-engine = myisam >> /etc/mysql/conf.d/noinnodb.cnf

