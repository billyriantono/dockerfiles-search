FROM balchu/ubuntu-with-vim

MAINTAINER chuabal@gmail.com loneranger

ENV FOO bar

RUN apt-get update
RUN apt-get dist-upgrade -y
RUN DEBIAN_FRONTEND=noninteractive apt-get -y dist-upgrade
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install python-software-properties
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install software-properties-common
RUN add-apt-repository ppa:webupd8team/java -y \
    && echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections \
    && apt-get update && apt-get install -y --force-yes --no-install-recommends \
    oracle-java8-installer \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN apt-get update
RUN apt-get install -y iputils-ping
WORKDIR /home/java

COPY src/HelloWorld.java .
RUN javac HelloWorld.java

VOLUME ["/data/myvol"]

ENTRYPOINT ["java","-cp",".",  "HelloWorld"]

