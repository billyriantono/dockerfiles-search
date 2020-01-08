FROM ubuntu:18.04
MAINTAINER Taewan Kim <taewanme@gmail.com>

RUN apt-get update
RUN apt-get install -y alien libaio1 wget openjdk-11-jdk python3.6 python3-pip
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/*

ENV ORACLINET_URL https://download.oracle.com/otn_software/linux/instantclient/193000/oracle-instantclient19.3-basic-19.3.0.0.0-1.x86_64.rpm
ENV SQLPLUS_URL https://download.oracle.com/otn_software/linux/instantclient/193000/oracle-instantclient19.3-sqlplus-19.3.0.0.0-1.x86_64.rpm
ENV CLI_VERSION 2.6.2

RUN wget ${ORACLINET_URL}
RUN wget ${SQLPLUS_URL}
RUN alien -i ./oracle-instantclient19.3-basic-19.3.0.0.0-1.x86_64.rpm
RUN alien -i ./oracle-instantclient19.3-sqlplus-19.3.0.0.0-1.x86_64.rpm
RUN echo '/usr/lib/oracle/19.3/client64/lib' > /etc/ld.so.conf.doracle-instantclient.conf
RUN ldconfig
RUN rm -rf oracle-instantclient*
RUN wget -qO- -O oci-cli.zip "https://github.com/oracle/oci-cli/releases/download/v${CLI_VERSION}/oci-cli-${CLI_VERSION}.zip"
RUN jar -xvf ./oci-cli.zip ./
RUN pip3 install ./oci-cli/oci_cli-*-py2.py3-none-any.whl
RUN rm -rf ./oci-cli
RUN rm -rf ./oci-cli.zip

ENV JAVA_HOME JAVA_HOME /usr/lib/jvm/java-11-openjdk-amd64


ENV ORACLE_HOME=/usr/lib/oracle/19.3/client64
ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8
