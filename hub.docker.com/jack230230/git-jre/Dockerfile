# Base
FROM java:7-jre

RUN sed -i 's/archive.ubuntu.com/cn.archive.ubuntu.com/' /etc/apt/sources.list

RUN apt-get update

RUN apt-get install -y wget build-essential automake openssh-client zlib1g-dev gettext libreadline-dev libssl-dev

# COPY ./v2.4.5.tar.gz git-2.4.5.tar.gz

RUN wget https://github.com/git/git/archive/v2.4.5.tar.gz -O git-2.4.5.tar.gz

RUN tar -zxf git-2.4.5.tar.gz 

RUN cd git-2.4.5 && autoconf && ./configure --without-tcltk && make && make install

RUN ln -s /usr/local/bin/git /usr/bin/git
