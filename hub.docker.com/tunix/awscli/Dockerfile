FROM debian:jessie-slim
MAINTAINER Alper Kanat <me@alperkan.at>

RUN echo "Europe/Istanbul" | tee /etc/timezone && \
    dpkg-reconfigure --frontend noninteractive tzdata && \
    mkdir /aws && \
    sed -i 's/deb.debian.org/ftp.tr.debian.org/g' /etc/apt/sources.list && \
    sed -i 's/security.debian.org/ftp.tr.debian.org\/debian-security/g' /etc/apt/sources.list

RUN apt-get update && \
    apt-get install -qqy libyaml-dev python3-pip zip curl && \
    curl -sL https://deb.nodesource.com/setup_6.x | bash - && \
    apt-get install -qqy nodejs=6.9.2-1nodesource1~jessie1 && \
    pip3 install awscli && \
    apt-get -qqy clean && apt-get -qqy autoclean && apt-get -qqy autoremove

WORKDIR /aws

CMD ["aws"]
