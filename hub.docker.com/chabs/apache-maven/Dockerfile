FROM busybox

MAINTAINER Cédric CLOVEL

RUN wget http://wwwftp.ciril.fr/pub/apache/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz -O /tmp/apache-maven.tar.gz -q && \
    mkdir -p /apache-maven && \
    tar -xf /tmp/apache-maven.tar.gz --strip-components=1 -C /apache-maven && \
    rm /tmp/apache-maven.tar.gz
