FROM mysql
MAINTAINER Viktor Voronin <voronin@x12.su>
RUN sed -i -e's/pid-file/innodb_use_native_aio=0\npid-file/' /etc/mysql/my.cnf
