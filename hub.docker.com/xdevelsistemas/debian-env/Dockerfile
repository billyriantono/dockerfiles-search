FROM debian:latest
MAINTAINER Clayton Santos da Silva "clayton@xdevel.com.br"

RUN apt-get update &&\
    apt-get install -y openssh-server &&\
    apt-get install -y sudo &&\
    echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu precise main" >> /etc/apt/sources.list && \
    TMPNAME=$(tempfile) && \
    apt-get update >> /dev/null 2> $TMPNAME && \
    PGPKEY=`cat $TMPNAME | cut -d":" -f6 | cut -d" " -f3` && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys $PGPKEY && \
    rm $TMPNAME && \
    apt-get update && \
    echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
    echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections && \
    DEBIAN_FRONTEND=noninteractive  apt-get install -yq oracle-java7-installer oracle-java7-set-default  && \
    #Clean up apt-repository
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
