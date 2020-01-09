FROM ubuntu
RUN apt update
RUN apt install -y wget unzip
WORKDIR /apps

RUN wget -O openjre.tar.gz https://github.com/AdoptOpenJDK/openjdk8-binaries/releases/download/jdk8u222-b10/OpenJDK8U-jre_x64_linux_hotspot_8u222b10.tar.gz
RUN tar -xvf openjre.tar.gz --one-top-level=openjre --strip-components=1
RUN rm openjre.tar.gz

ENV PATH="$PATH:/apps/openjre/bin"
ENV HOME /root
WORKDIR $HOME
