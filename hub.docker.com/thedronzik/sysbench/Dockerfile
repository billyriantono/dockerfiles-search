FROM ubuntu:latest

MAINTAINER thedronzik <thedronzik@gmail.com>

#RUN apt -yq install libc6:i386 libstdc++6:i386 zlib1g:i386 libncurses5:i386 curl bzip2 xz-utils wget tar unzip git --no-install-recommends && \
RUN apt-get -qq update
RUN apt-get -y install curl
RUN curl -s https://packagecloud.io/install/repositories/akopytov/sysbench/script.deb.sh | bash
RUN apt -y install sysbench
    
ENTRYPOINT ["/usr/bin/sysbench"]