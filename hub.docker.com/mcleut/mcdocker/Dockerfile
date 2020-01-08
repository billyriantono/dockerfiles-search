FROM ubuntu:latest
MAINTAINER Christopher Leuthardt <mail@christopher-leuthardt.de>

ENV DEBIAN_FRONTEND noninteractive
ENV TERM xterm-256color

RUN rm -rf /etc/apt/sources.*
RUN echo "deb http://de.archive.ubuntu.com/ubuntu/ cosmic main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src http://de.archive.ubuntu.com/ubuntu/ cosmic main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb http://security.ubuntu.com/ubuntu cosmic-security main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src http://security.ubuntu.com/ubuntu cosmic-security main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb http://de.archive.ubuntu.com/ubuntu/ cosmic-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src http://de.archive.ubuntu.com/ubuntu/ cosmic-updates main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb http://de.archive.ubuntu.com/ubuntu/ cosmic-backports main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb-src http://de.archive.ubuntu.com/ubuntu/ cosmic-backports main restricted universe multiverse" >> /etc/apt/sources.list && \
    echo "deb http://archive.canonical.com/ubuntu cosmic partner" >> /etc/apt/sources.list && \
    echo "deb-src http://archive.canonical.com/ubuntu cosmic partner" >> /etc/apt/sources.list
RUN apt update -q -y && apt dist-upgrade -q -y && apt autoremove -q -y && apt clean all && \
    apt install -y wget cron tzdata openjdk-11-jre screen

RUN echo "0  2    * * *   root    apt update -q -y && apt dist-upgrade -q -y && apt autoremove -q -y && apt clean all" >> /etc/crontab
RUN update-rc.d cron defaults
RUN /etc/init.d/cron restart

RUN ln -fs /usr/share/Europe/Berlin /etc/localtime
RUN dpkg-reconfigure --frontend noninteractive tzdata

RUN mkdir /home/MC/ && useradd -d /home/MC/ MC && chown MC /home/MC/
RUN cd /home/MC/ && \
    wget https://christopher-leuthardt.de/files/MCServer.jar && \
    chmod 744 /home/MC/MCServer.jar && \
    wget https://christopher-leuthardt.de/files/MCStart.sh && \
    chmod 744 /home/MC/MCStart.sh && \
    ./MCStart.sh && \
    rm -rf eula.txt && touch eula.txt && \
    echo "eula=true" >> /home/MC/eula.txt && ./MCStart.sh
