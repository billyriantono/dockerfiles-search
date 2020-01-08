FROM centos:7
LABEL maintainer="kwonghung.yip@gmail.com"
ENV version=12.2.0.1.0

RUN mkdir -p /opt/oracle

COPY packages/oracle-instantclient12.2-basic-${version}-1.x86_64.rpm /opt/oracle
COPY packages/oracle-instantclient12.2-devel-${version}-1.x86_64.rpm /opt/oracle
COPY packages/oracle-instantclient12.2-jdbc-${version}-1.x86_64.rpm /opt/oracle
COPY packages/oracle-instantclient12.2-odbc-${version}-2.x86_64.rpm /opt/oracle
COPY packages/oracle-instantclient12.2-sqlplus-${version}-1.x86_64.rpm /opt/oracle
COPY packages/oracle-instantclient12.2-tools-${version}-1.x86_64.rpm /opt/oracle

RUN yum -y install /opt/oracle/oracle-instantclient12.2-basic-${version}-1.x86_64.rpm
RUN yum -y install /opt/oracle/oracle-instantclient12.2-devel-${version}-1.x86_64.rpm
RUN yum -y install /opt/oracle/oracle-instantclient12.2-jdbc-${version}-1.x86_64.rpm
RUN yum -y install /opt/oracle/oracle-instantclient12.2-odbc-${version}-2.x86_64.rpm
RUN yum -y install /opt/oracle/oracle-instantclient12.2-sqlplus-${version}-1.x86_64.rpm
RUN yum -y install /opt/oracle/oracle-instantclient12.2-tools-${version}-1.x86_64.rpm

RUN sh -c "echo /usr/lib/oracle/12.2/client64/lib > /etc/ld.so.conf.d/oracle-instantclient.conf" 
RUN ldconfig 

ENV LD_LIBRARY_PATH=/opt/oracle/instantclient_12_2:${LD_LIBRARY_PATH}
RUN mkdir -p /usr/lib/oracle/12.2/client64/lib/network/admin

ENV PATH=/usr/lib/oracle/12.2/client64/bin:${PATH}

COPY tnsnames.ora /usr/lib/oracle/12.2/client64/lib/network/admin

RUN mkdir -p /opt/oracle/sql
COPY sql/testconn.sql /opt/oracle/sql

WORKDIR /opt/oracle/sql

#ENTRYPOINT ["sqlplus"]

CMD ["bash"]