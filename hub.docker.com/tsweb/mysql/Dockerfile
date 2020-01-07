FROM tsweb/centos64
MAINTAINER Kazuhisa Kumagai <k-kumagai@ts.tv-osaka.co.jp>

EXPOSE 3306

#--------------------------------------
# initialize
#--------------------------------------

RUN yum -y install wget
RUN yum -y install tar gcc

#--------------------------------------
# install MySQL 5.5.28
#--------------------------------------

# resolving dependence
RUN yum -y install ncurses-devel cmake gcc-c++

# useradd
RUN groupadd mysql
RUN useradd -g mysql -s /sbin/nologin mysql

# download
RUN (\
	cd /usr/local/src;\
	wget http://downloads.mysql.com/archives/mysql-5.5/mysql-5.5.28.tar.gz;\
	tar xvzf mysql-5.5.28.tar.gz;\
	cd mysql-5.5.28;\
	cmake . \
		-DCMAKE_INSTALL_PREFIX=/usr/local/mysql \
		-DDEFAULT_CHARSET=utf8 \
		-DDEFAULT_COLLATION=utf8_general_ci \
		-DWITH_EXTRA_CHARSETS=all \
		-DWITH_INNOBASE_STORAGE_ENGINE=1 \
		-DENABLED_LOCAL_INFILE=1;\
	make;\
	make install;\
	make clean;\
	cp -f /usr/local/mysql/support-files/mysql.server /etc/rc.d/init.d/mysqld;\
	chmod +x /etc/rc.d/init.d/mysqld;\
)

# chown
RUN chown -R mysql:mysql /usr/local/mysql

# path to mysqldir
ENV PATH $PATH:/usr/local/mysql/bin

# copy conffile
RUN \cp -f /usr/local/mysql/support-files/my-medium.cnf /etc/my.cnf

#--------------------------------------
# initialize
#--------------------------------------

# install initializer
RUN mkdir /root/scripts
ADD service.sh /root/scripts/service.sh
RUN chmod +x /root/scripts/*.sh

# run service
CMD ["/root/scripts/service.sh"]
