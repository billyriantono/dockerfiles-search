FROM ubuntu:latest

## Install required system packages first
RUN apt-get update && \
  apt-get -f dist-upgrade -y && sync && \
  apt-get install -y sudo tar perl unzip p7zip-full vim curl wget rsync git socat ctags \
  openjdk-8-jdk-headless g++ make automake autoconf libtool intltool cmake colormake htop && \
  dpkg --configure -a && \
  apt-get auto-remove && apt-get remove && apt-get clean

## Create system user to run the intended apps and/or services and, add the user to system groups
RUN adduser --system --shell /bin/bash --gecos 'Muster Manager' --group --disabled-password --home /home/musterer musterer && \
  usermod -a -G adm,cdrom,sudo,dip,plugdev musterer && sync

## Copy customer user settings to user home
COPY --chown=musterer:musterer dotcfg/* /home/musterer/
COPY --chown=musterer:musterer vimmods /home/musterer/.vim
COPY --chown=musterer:musterer tools /home/musterer/tools

## Set working directory to ubuntu user
USER musterer
WORKDIR /home/musterer

## Install 'n' script and then, install Node.js from 'n' script
ENV N_PREFIX="/home/musterer/tools/n"
RUN curl -L https://git.io/n-install -o n-install.sh && bash n-install.sh -y && \
  export PATH=${N_PREFIX}/bin:$PATH && n stable && n prune && sync && \
  npm install -g npm pm2 nodemon npm-check eslint typescript && mkdir deploy

## Extract pre-built packages
WORKDIR /home/musterer/tools
RUN curl -L https://dl.google.com/go/go1.12.7.linux-amd64.tar.gz -o pkg.tgz && tar -zxvf pkg.tgz && sync && rm -f pkg.tgz && \
  curl -L http://us.mirrors.quenda.co/apache/maven/maven-3/3.6.1/binaries/apache-maven-3.6.1-bin.tar.gz -o pkg.tgz && tar -zxvf pkg.tgz && sync && rm -f pkg.tgz && \
  curl -L https://dl.bintray.com/groovy/maven/apache-groovy-sdk-2.5.7.zip -o pkg.zip && unzip pkg.zip && sync && rm -f pkg.zip && \
  curl -L https://services.gradle.org/distributions/gradle-5.5.1-bin.zip -o pkg.zip && unzip pkg.zip && sync && rm -f pkg.zip && \
  mv groovy-2.5.7 groovy && mv gradle-5.5.1 gradle && mv apache-maven-3.6.1 maven && rm -f ../n-install.sh && sync
WORKDIR /home/musterer
