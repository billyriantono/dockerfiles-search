FROM tsweb/centos64
MAINTAINER Kazuhisa Kumagai <k-kumagai@ts.tv-osaka.co.jp>

EXPOSE 5432

#--------------------------------------
# initialize
#--------------------------------------

RUN yum -y install wget
RUN yum -y install tar gcc
RUN yum -y install zlib-devel

#--------------------------------------
# install PostgreSQL 8.4.4
#--------------------------------------

# resolving dependence
RUN yum -y install readline-devel

# useradd
RUN groupadd postgres
RUN useradd -g postgres postgres
RUN echo "postgres ALL=(ALL) NOPASSWD:/usr/local/pgsql/bin/initdb" >> /etc/sudoers

# download and install
RUN (\
	cd /usr/local/src;\
	wget -O postgresql-8.4.4.tar.gz ftp://ftp.postgresql.org/pub/source/v8.4.4/postgresql-8.4.4.tar.gz;\
	tar zxvf postgresql-8.4.4.tar.gz;\
	cd postgresql-8.4.4;\
	./configure --prefix=/usr/local/pgsql;\
	make;\
	make install;\
	make clean;\
	cp -f ./contrib/start-scripts/linux /etc/rc.d/init.d/postgres;\
	chmod +x /etc/rc.d/init.d/postgres;\
)

# chown
RUN mkdir /usr/local/pgsql/data
RUN chown -R postgres:postgres /usr/local/pgsql

# path to pgsqldir
ENV PATH $PATH:/usr/local/pgsql/bin
ENV POSTGRES_HOME /usr/local/pgsql
ENV PGLIB $POSTGRES_HOME/lib
ENV PGDATA $POSTGRES_HOME/data
ENV MANPATH "$MANPATH":$POSTGRES_HOME/man
ENV LD_LIBRARY_PATH "$LD_LIBRARY_PATH":"$PGLIB"

#--------------------------------------
# initialize
#--------------------------------------

# install initializer
RUN mkdir /root/scripts
ADD service.sh /root/scripts/service.sh
RUN chmod +x /root/scripts/*.sh

# run service
CMD ["/root/scripts/service.sh"]
