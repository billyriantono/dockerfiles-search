FROM ubuntu:16.04

RUN mkdir /var/novacoin
WORKDIR /var/novacoin

RUN echo "deb http://archive.ubuntu.com/ubuntu/ trusty main restricted universe multiverse" >> /etc/apt/sources.list
RUN echo "deb-src http://archive.ubuntu.com/ubuntu/ trusty main restricted universe multiverse" >> /etc/apt/sources.list

RUN apt-get update

RUN apt-get install -y \
    wget curl

RUN cd /var/novacoin
RUN mkdir downloaded && cd downloaded

RUN curl https://netcologne.dl.sourceforge.net/project/novacoin/novacoin-0.5.7/deb/novacoind_0.5.7~377ff13a-1_amd64.deb -o /var/novacoin/downloaded/install.deb
RUN dpkg -i /var/novacoin/downloaded/install.deb; exit 0
RUN apt-get install -fy

RUN apt-get install gosu -y

COPY entrypoint.sh /usr/local/bin/entrypoint.sh

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
CMD novacoind