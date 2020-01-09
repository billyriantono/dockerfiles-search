FROM ashtreecc/ubuntu:16.10

MAINTAINER Andrew Nash "akahadaka@gmail.com"

RUN curl https://nodejs.org/download/release/v6.5.0/node-v6.5.0-linux-x64.tar.gz | tar xz -C /usr/local/ --strip=1

# Fix node vs nodejs being different
RUN update-alternatives --install /usr/local/bin/node node /usr/bin/nodejs 10

VOLUME /src
WORKDIR /src
