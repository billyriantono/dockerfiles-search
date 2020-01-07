FROM centos:7
RUN yum update -y && yum install -y gcc && yum install -y make
RUN rm /usr/bin/sqlite3
RUN curl -o sqlite-autoconf-3290000.tar.gz https://www.sqlite.org/2019/sqlite-autoconf-3290000.tar.gz
RUN tar zxvf sqlite-autoconf-3290000.tar.gz && cd sqlite-autoconf-3290000 && ./configure --prefix=/opt/sqlite && make && make install && cp /opt/sqlite/bin/sqlite3 /usr/bin/
WORKDIR /root/db
ENTRYPOINT ["sqlite3"]