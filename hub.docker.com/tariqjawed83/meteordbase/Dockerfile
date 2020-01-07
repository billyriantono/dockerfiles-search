FROM abernix/meteord:base

MAINTAINER Tariq Jawed

RUN echo "deb http://ftp.debian.org/debian jessie-backports main" >> /etc/apt/sources.list 
RUN mkdir -p /apps/wkhtmltox \
 mkdir /tmp

COPY wkhtmltox-0.12.4_linux-generic-amd64.tar.xz /tmp

RUN tar xf /tmp/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz -C /apps 
RUN apt-get clean \
 && apt-get update -y \
 && apt-get install -y libxrender1 \
 && apt-get install -y fontconfig \
 && apt-get install -y -t jessie-backports unoconv 
RUN rm -rf /tmp

ENV PATH=/apps/wkhtmltox/bin:$PATH
