FROM ubuntu:18.04
LABEL version="3.0"
LABEL name="base"

ENV USER=webuser
COPY start.sh /usr/local/bin/start.sh


RUN apt update && \
 apt install -y gnupg2 && \
 apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 4F4EA0AAE5267A6C && \
 apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 3B4FE6ACC0B21F32 && \
 apt update -y && \
 apt upgrade -y && \
 apt install \
      git \
      iputils-ping \
      mcrypt \
      libmhash2 \
      openssl \
      patch \
      unzip \
      zip \
      lsof  \
      mysql-client -y && \
 apt clean all

COPY ondrej-ubuntu* /etc/apt/sources.list.d/

RUN chmod +x /usr/local/bin/start.sh
ENTRYPOINT [ "/usr/local/bin/start.sh" ]
