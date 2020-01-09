FROM debian:jessie-slim

# production
RUN echo "\n\
deb http://ftp.debian.org/debian jessie main\n\
\ndeb http://ftp.us.debian.org/debian testing main contrib non-free" >> /etc/apt/sources.list

RUN apt-get update
RUN apt-get install -y curl gcc-7 g++-7 cmake

# Yarn
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get install -y nodejs

RUN apt-get remove -y curl
RUN apt-get purge -y curl
RUN apt-get autoremove -y

RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 100 --slave /usr/bin/g++ g++ /usr/bin/g++-7
