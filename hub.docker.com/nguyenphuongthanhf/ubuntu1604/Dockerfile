# Create the container:
# - docker run -t -i --name xxx anphabe/base:14.04 /bin/bash
#
FROM ubuntu:16.04


# APT upgrade
RUN DEBIAN_FRONTEND=noninteractive apt-get -y update
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_CTYPE en_US.UTF-8

RUN DEBIAN_FRONTEND=noninteractive apt-get install --reinstall -y apt-transport-https locales language-pack-en-base  && \
    locale-gen en_US && \
    locale-gen en_US.UTF-8 && \
    dpkg-reconfigure locales
# fix user environment
RUN echo "alias ll='ls -alh'" >> /etc/bash.bashrc && \
    mv /etc/localtime /etc/localtime.bk && \
    ln -s /usr/share/zoneinfo/Asia/Ho_Chi_Minh /etc/localtime
RUN DEBIAN_FRONTEND=noninteractive apt-get upgrade -y && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y sudo software-properties-common python-software-properties vim wget curl unzip
