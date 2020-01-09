FROM debian:9

MAINTAINER Juan Jose Aparicio <aparicio_juan@hotmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get -y upgrade && apt-get install -y build-essential && \
    apt-get install git-core subversion libjansson-dev sqlite autoconf automake libtool libxml2-dev libncurses5-dev wget git -y && apt-get install -y apt-utils && \
    cd /usr/src/ && wget http://downloads.asterisk.org/pub/telephony/asterisk/asterisk-13-current.tar.gz && \
    tar -xzvf asterisk-13-current.tar.gz && rm *.tar.gz && mv asterisk* asterisk/ && cd asterisk/ &&  \
    echo yes | ./contrib/scripts/install_prereq install && ./contrib/scripts/get_mp3_source.sh && \
    ./configure --with-pjproject-bundled && \
    make menuselect.makeopts && \
    menuselect/menuselect --disable BUILD_NATIVE menuselect.makeopts && \
    sed -i "s/BUILD_NATIVE //" menuselect.makeopts && \
    menuselect/menuselect --list-options && \
    make NOISY_BUILD=yes && \
    make install && make config && apt-get clean && apt-get autoclean && rm -rf /var/lib/apt/lists/*

CMD ["/usr/sbin/asterisk", "-f"]

EXPOSE 5060/tcp
EXPOSE 10000-20000/udp
