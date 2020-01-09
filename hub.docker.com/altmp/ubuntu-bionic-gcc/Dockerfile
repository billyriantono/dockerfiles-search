FROM ubuntu:18.04

RUN apt-get update
RUN apt-get install -y curl cmake gcc-8 g++-8

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get install -y nodejs

RUN apt-get remove -y curl
RUN apt-get purge -y curl
RUN apt-get autoremove -y

RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 100 --slave /usr/bin/g++ g++ /usr/bin/g++-8
RUN rm -rf /usr/local/man
RUN rm -rf /var/lib/apt/lists/*
