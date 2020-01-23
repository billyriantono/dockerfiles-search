FROM debian:8
MAINTAINER W Brune "github@brune.biz"
# ORIGINAL MAINTAINER Tobias Mandjik "webmaster@leckerbeef.de"
# ORIGINAL MAINTAINER Felix Bartels "felix@host-consultants.de"

ENV DEBIAN_FRONTEND noninteractive
ENV MYSQLTMPROOT topSecret

RUN apt-get update -qq -y && apt-get install -qq -y \
    wget \
    apt-utils \
    debconf 

RUN echo mysql-server mysql-server/root_password password $MYSQLTMPROOT | debconf-set-selections; \
    echo mysql-server mysql-server/root_password_again password $MYSQLTMPROOT| debconf-set-selections; \
    apt-get update -qq -y && apt-get install -y --force-yes \
    mysql-server \
    apache2 

RUN  mkdir -p /root/packages \
     && cd /root/packages \
     && wget -q https://download.zarafa.com/community/final/7.2/7.2.4.29/zcp-7.2.4.29-ubuntu-15.04-x86_64-community.tar.gz -O- | tar xz --strip-components=1 \
     && apt-ftparchive packages . | gzip -9c > Packages.gz \
     && echo "deb file:/root/packages /" > /etc/apt/sources.list.d/zarafa.list \
     && service apache2 start \
     && apt-get  update -qq -y && apt-get install -qq -y --force-yes php5-mapi zarafa \
     && rm /root/packages/* \
     && rmdir /root/packages \
     && apt-get clean 
