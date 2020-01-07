FROM python:2.7.14


ADD oracle/instantclient-basic-linux.x64-12.1.0.2.0.zip /tmp
ADD oracle/instantclient-sdk-linux.x64-12.1.0.2.0.zip /tmp
ADD oracle/instantclient-sqlplus-linux.x64-12.1.0.2.0.zip /tmp

RUN  apt-get -y update 
RUN  apt-get -y upgrade
RUN  apt-get install -y unzip

RUN unzip /tmp/instantclient-basic-linux.x64-12.1.0.2.0.zip -d /usr/local/
RUN unzip /tmp/instantclient-sdk-linux.x64-12.1.0.2.0.zip -d /usr/local/
RUN unzip /tmp/instantclient-sqlplus-linux.x64-12.1.0.2.0.zip -d /usr/local/

RUN ln -s /usr/local/instantclient_12_1 /usr/local/instantclient
RUN ln -s /usr/local/instantclient/libclntsh.so.12.1 /usr/local/instantclient/libclntsh.so
RUN ln -s /usr/local/instantclient/sqlplus /usr/bin/sqlplus


RUN apt-get install -y build-essential  libaio-dev  zlib1g-dev  libjpeg-dev

ENV ORACLE_HOME /usr/local/instantclient
ENV LD_LIBRARY_PATH /usr/local/instantclient
ENV TNS_ADMIN /usr/local/instantclient/network/admin

EXPOSE 8000