FROM ubuntu:18.04
MAINTAINER Steyn Geldenhuys "steyn@truevolve.technology"

USER root
RUN apt-get update && \
    apt-get install -y gtk2-engines libxtst6 libxxf86vm1 freeglut3 libxslt1.1 libcanberra-gtk-module g++ gcc libc6-dev make curl libpcre3-dev vim git sudo build-essential mingw-w64 cmake curl swig gcc-arm-linux-gnueabihf g++-arm-linux-gnueabihf && \
    apt-get clean && apt-get purge && apt-get autoremove


RUN mkdir -p /home/developer/ && \
    echo "developer:x:1000:1000:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
    echo "developer:x:1000:" >> /etc/group && \
    echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
    chmod 0440 /etc/sudoers.d/developer && \
    chown developer:developer -R /home/developer

USER developer

ENV GOLANG_VERSION 1.12.5
ENV GOLANG_DOWNLOAD_URL https://golang.org/dl/go$GOLANG_VERSION.linux-amd64.tar.gz

WORKDIR /home/developer/
RUN curl -kfsSL "$GOLANG_DOWNLOAD_URL" -o golang.tar.gz \
	&& tar -C /home/developer/ -xzf golang.tar.gz \
	&& rm golang.tar.gz

RUN curl https://download-cf.jetbrains.com/go/goland-2019.1.2.tar.gz -o /home/developer/goland.tar.gz

RUN  mkdir /home/developer/goland && \
     tar -xvzf /home/developer/goland.tar.gz -C /home/developer/goland --strip-components 1 && \
     rm /home/developer/goland.tar.gz

ENV GOROOT /home/developer/go
ENV GOPATH /home/developer/
ENV PATH $GOROOT/bin:$PATH
ENV HOME /home/developer
WORKDIR /home/developer
CMD cd /home/developer/goland/bin/ && ./goland.sh
