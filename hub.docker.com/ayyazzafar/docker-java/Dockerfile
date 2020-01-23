FROM ubuntu:xenial

LABEL MAINTAINER="Ayyaz Zafar <contact@ayyaz.io>"

ENV DEBIAN_FRONTEND=noninteractive \
    TERM=xterm

RUN buildDeps='software-properties-common'; \
    set -x && \
    apt-get -qq update && apt-get -qq install -y $buildDeps --no-install-recommends && \
    # use WebUpd8 PPA
    add-apt-repository ppa:webupd8team/java -y && \
    apt-get -qq update -y && \
    # automatically accept the Oracle license
    echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
    apt-get -qq install -y oracle-java8-installer && \
    apt-get -qq install -y oracle-java8-set-default && \
    # clean up
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    apt-get purge -y --auto-remove $buildDeps && \
    apt-get autoremove -y && apt-get clean

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle
