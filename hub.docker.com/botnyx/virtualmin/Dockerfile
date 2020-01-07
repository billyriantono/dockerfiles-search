FROM ubuntu:16.04

MAINTAINER Jerry Hopper <hopper.jerry@gmail.com>


# Install.
RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y build-essential && \
  apt-get install -y software-properties-common && \
  apt-get install -y byobu curl git htop man unzip vim wget && \
  rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y locales && rm -rf /var/lib/apt/lists/* && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
ENV LANG en_US.utf8

# Set environment variables.
ENV HOME /root

# Define working directory.
#WORKDIR /root

# Set root password to 'admin'
RUN printf admin\\nadmin\\n | passwd

# RUN wget http://software.virtualmin.com/gpl/scripts/install.sh && sh install.sh -f --hostname localhost

EXPOSE 22 25 10000 10001 10002 10003 10004 10005 10006 10007 10008 10009 20000
EXPOSE 80 443 21 20 110 143
EXPOSE 53/udp 53/tcp

#CMD ["/etc/webmin/start"]

ENTRYPOINT ["bash"]
