FROM ubuntu:latest
MAINTAINER Zehuan Li
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y net-tools wget curl socat iputils-ping traceroute lsof zip sudo
RUN apt-get install -y vim python3-dev python3-setuptools python3-pip python-dev python-setuptools python-pip
RUN apt-get install -y build-essential gcc-multilib gdb
RUN apt-get install -y git-core
RUN apt-get install -y nmap

WORKDIR /root
RUN git clone https://github.com/darkoperator/dnsrecon.git && \
    git clone https://github.com/ChrisTruncer/EyeWitness.git && \
    git clone https://github.com/SpiderLabs/Responder.git && \
    git clone --depth 1 https://github.com/drwetter/testssl.sh.git
RUN curl https://raw.githubusercontent.com/rapid7/metasploit-omnibus/master/config/templates/metasploit-framework-wrappers/msfupdate.erb > msfinstall && \
  chmod 755 msfinstall && \
  ./msfinstall && \
  rm -rf msfinstall
