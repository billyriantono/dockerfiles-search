FROM debian:9.6

RUN apt-get update
RUN apt-get install -y software-properties-common openssh-server sudo vim dos2unix wget unzip git curl bzip2 gcc g++ binutils make autoconf openssl libssl-dev ant libopus0 libpcre3 libpcre3-dev build-essential nasm

RUN add-apt-repository -y ppa:webupd8team/java
RUN apt-get update
RUN apt-get purge -y openjdk*
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | sudo debconf-set-selections
RUN echo debconf shared/accepted-oracle-license-v1-1 seen true | sudo debconf-set-selections
RUN apt-get install -y --allow-unauthenticated oracle-java8-installer
RUN apt-get clean
RUN rm -fr /etc/apt/sources.list.d/webupd8team-ubuntu-java-disco.list

ENV BANANA_PASSWD=Mudar123

RUN mkdir /workspace

COPY ./tools/start-packages.sh /usr/local/bin/start-packages
RUN chmod +x  /usr/local/bin/start-packages \
    && dos2unix /usr/local/bin/start-packages

RUN useradd -ms /bin/bash banana && echo "banana:${BANANA_PASSWD}" | chpasswd
RUN echo "banana ALL=(ALL:ALL) ALL" >> /etc/sudoers
RUN chown -R banana:banana /workspace

RUN wget https://github.com/gleisonnanet/pjsip-android-builder/archive/master.zip \
    && unzip master.zip \
    && mv pjsip-android-builder-master /home/ \
    && rm -fr master.zip \
    && cp -R /home/pjsip-android-builder-master/* /home/ \
    && rm -fr /home/pjsip-android-builder-master

VOLUME [ "/workspace" ]

EXPOSE 22

CMD ["/usr/local/bin/start-packages"]
