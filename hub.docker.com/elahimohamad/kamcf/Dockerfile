FROM debian:stretch
ENV DEBIAN_FRONTEND noninteractive
RUN apt update
RUN apt install -y gcc g++ flex bison libmariadbclient-dev make libcurl3 autoconf libssl-dev libxml2-dev libpcre3 libmnl-dev libunistring-dev
RUN apt install -y mariadb-client

ADD https://github.com/kamailio/kamailio/archive/5.2.1.tar.gz /
RUN tar -xvf 5.2.1.tar.gz
RUN mv /kamailio-5.2.1 /kamailio

EXPOSE 5060
