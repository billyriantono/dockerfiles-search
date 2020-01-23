FROM ubuntu:16.10
MAINTAINER Borja Maceira <ant@antweb.es>
ENV REFRESHED_AT 2016-09-22
ENV VERSION 0.0.1
ENV DEBIAN_FRONTEND noninteractive 
ENV INSPIRCD_SRC_VERSION 2.0.23


RUN apt-get update && apt-get install -y -o Dpkg::Options::="--force-confdef" \
    pkg-config \
    build-essential \
    gnutls-bin \
    libgnutls28-dev \
    openssl \
    libssl-dev \
    libssl1.0.0 \
    curl \
    unzip \
    libpcre3 \
    libpcre3-dev \
    libmysqlclient-dev \
    libgeoip-dev \
    --no-install-recommends && rm -r /var/lib/apt/lists/*
    

RUN curl -s --location https://github.com/inspircd/inspircd/archive/v$INSPIRCD_SRC_VERSION.tar.gz --insecure | tar xz

RUN mkdir /src/ && \
    mv inspircd-$INSPIRCD_SRC_VERSION /src/ && \
    useradd -u 10000 -d /inspircd/ inspircd && \
    cd /src/inspircd-$INSPIRCD_SRC_VERSION/ && \
    ./configure --enable-extras m_mysql.cpp && \
    ./configure --enable-extras m_regex_pcre.cpp  && \
    ./configure --enable-extras m_regex_posix.cpp && \
    ./configure --enable-extras m_regex_stdlib.cpp  && \
    ./configure --enable-extras m_ssl_gnutls.cpp && \
    ./configure --enable-extras m_ssl_openssl.cpp && \
    ./configure --enable-extras m_geoip.cpp  && \
    ./configure --disable-interactive --prefix=/inspircd --uid 10000 --enable-gnutls --enable-epoll && \
    make  && make install
    
ADD conf/inspircd.conf      /inspircd/conf/inspircd.conf
ADD conf/inspircd.motd      /inspircd/conf/inspircd.motd
ADD conf/inspircd.rules     /inspircd/conf/inspircd.rules
ADD conf/links.conf         /inspircd/conf/links.conf
ADD conf/modules.conf       /inspircd/conf/modules.conf
ADD conf/opers.conf         /inspircd/conf/opers.conf
ADD conf/permchannels.conf  /inspircd/conf/permchannels.conf

ADD conf/limits.conf /etc/security/limits.d/inspircd.conf

VOLUME ["/inspircd/logs", "/inspircd/conf", "/inspircd/modules"]

EXPOSE 6667

ENTRYPOINT ["/inspircd/bin/inspircd", "--nofork", "--runasroot"]

CMD [""]


