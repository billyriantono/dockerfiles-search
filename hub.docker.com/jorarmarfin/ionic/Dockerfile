FROM ubuntu:16.04

# Environments vars
ENV DEBIAN_FRONTEND noninteractive
ENV TERM=xterm \
    VERSION=10.16.3 \
    DISTRO=linux-x64

RUN apt-get update && apt-get -y upgrade; \
    apt-get install -y vim python3 wget;
#INSTALACION NODE JS
RUN apt-get -y install xz-utils \
    && wget https://nodejs.org/dist/v$VERSION/node-v$VERSION-$DISTRO.tar.xz \
    && mkdir -p /usr/local/lib/nodejs \
    && tar -xJvf node-v$VERSION-$DISTRO.tar.xz -C /usr/local/lib/nodejs \
    && echo 'VERSION=v'$VERSION>>/root/.profile \
    && echo 'DISTRO='$DISTRO>>/root/.profile \
    && echo 'export PATH=/usr/local/lib/nodejs/node-v'$VERSION'-'$DISTRO'/bin:$PATH'>>/root/.profile \
    && ln -s /usr/local/lib/nodejs/node-v$VERSION-$DISTRO/bin/node /usr/bin/node \
    && ln -s /usr/local/lib/nodejs/node-v$VERSION-$DISTRO/bin/npm /usr/bin/npm \
    && ln -s /usr/local/lib/nodejs/node-v$VERSION-$DISTRO/bin/npx /usr/bin/npx \
    && . /root/.profile \
    ##Instala Ionic
    && npm install -g ionic


# Init
ADD init.sh /init.sh
RUN chmod 755 /*.sh
EXPOSE 8100
CMD [ "/init.sh" ]