FROM java:8

MAINTAINER Sofian Hadiwijaya <me@sofianhw.com>

RUN apt-get update -y && \ 
    apt-get install --no-install-recommends -y \ 
    -q curl python build-essential git ca-certificates

RUN mkdir /nodejs && \
    curl https://nodejs.org/dist/latest/node-v5.7.0-linux-x64.tar.gz \ 
    | tar xvzf - -C /nodejs --strip-components=1

ENV PATH $PATH:/nodejs/bin

RUN apt-get install -y rlwrap

RUN curl https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein > /bin/lein
RUN chmod a+x /bin/lein

ENV LEIN_ROOT=1
RUN lein

WORKDIR /
