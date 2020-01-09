FROM ubuntu:disco

ARG antlr4_version=4.7.2

# If run Docker behind a corporate proxy, set it here
#ENV http_proxy
#ENV https_proxy
#ENV HTTP_PROXY
#ENV HTTPS_PROXY
#ENV ftp_proxy
#ENV socks_proxy
#ENV no_proxy

# make sure we're up-to-date
RUN apt-get -y update && apt-get -y upgrade 

# set the locale
RUN apt-get -y update && apt-get -y install locales
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && locale-gen
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# install everything we need for Yocto builds
RUN apt-get -y update && apt-get -y install gawk wget git-core diffstat unzip texinfo gcc-multilib build-essential chrpath socat cpio python python3 python3-pip python3-pexpect xz-utils debianutils iputils-ping libsdl1.2-dev xterm
# install our other prereqs
RUN apt-get -y update && apt-get -y install libboost-all-dev libssl-dev cmake
RUN apt-get -y update && apt-get -y install default-jre

RUN wget https://www.antlr.org/download/antlr-${antlr4_version}-complete.jar -P /usr/local/lib
RUN wget https://www.antlr.org/download/antlr4-cpp-runtime-${antlr4_version}-source.zip -P /usr/local/lib
ADD antlr4/files/deploy.sh /usr/bin/deploy
RUN chmod +x /usr/bin/deploy
ADD antlr4/files/antlr4.sh /usr/bin/antlr4
RUN chmod +x /usr/bin/antlr4
ADD antlr4/files/grun.sh /usr/bin/grun
RUN chmod +x /usr/bin/grun
ENV CLASSPATH .:/usr/local/lib/antlr-${antlr4_version}-complete.jar:$CLASSPATH
