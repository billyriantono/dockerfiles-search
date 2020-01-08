FROM ubuntu:16.04
MAINTAINER Samina Fu <sufuf3[at]gmail.com>

ENTRYPOINT bash

# Env package install
ENV UBUNTU_APT_SITE free.nchc.org.tw
RUN sed -i 's/^deb-src\ /\#deb-src\ /g' /etc/apt/sources.list
RUN sed -E -i "s/([a-z]+.)?archive.ubuntu.com/$UBUNTU_APT_SITE/g" /etc/apt/sources.list
RUN sed -i "s/security.ubuntu.com/$UBUNTU_APT_SITE/g" /etc/apt/sources.list
RUN apt update         && \
    apt upgrade -y     && \
    DEBIAN_FRONTEND="noninteractive" apt install -y -o Dpkg::Options::="--force-confdef" -o Dpkg::Options::="--force-confold" \
        locales dnsutils openssh-server dpkg coreutils util-linux passwd bsdutils file \
        openssl ca-certificates ssh wget curl cpio dnsutils patch sudo sysstat vnstat  \
        htop dstat vim nano tmux ftp tree aptitude colordiff curl fail2ban mtr-tiny    \
        ntpdate git p7zip-full nmap apt-file command-not-found unzip tcpdump iftop cmake \
        iotop xterm unattended-upgrades ppa-purge jq iperf traceroute whois lsof iputils-ping \
        ufw make build-essential bash-completion python-pip python-dev build-essential \
        python-setuptools software-properties-common iperf3 mailutils net-tools \
        libsqlite3-dev libzmq3-dev python3 python3-pip python3-dev libsqlite3-dev libssl-dev zlib1g-dev supervisor screen && \
    rm -rf /var/lib/apt/lists/*


# pip install packages
RUN python3 -m pip install --upgrade pip
RUN pip install urllib3 virtualenv

# Install python3 & pip package
RUN pip3 install -U setuptools

# Add iottalk user
RUN useradd -m iottalk -s /bin/bash
RUN adduser iottalk sudo
RUN adduser iottalk adm
RUN chown -R iottalk:iottalk /home/iottalk
RUN echo '%iottalk ALL=(ALL) NOPASSWD: ALL' | sudo tee -a /etc/sudoers.d/iottalk

# Setup IoTtalk server backend
RUN cd /home/iottalk/ && sudo -u iottalk git clone https://github.com/sufuf3/k8s-IoTtalk.git iottalk_server_1.0
RUN cd /home/iottalk/iottalk_server_1.0 && sudo -u iottalk git checkout v1.0.0
RUN cd /home/iottalk/iottalk_server_1.0 && sudo -H pip3 install -r requirements.txt
RUN cd /home/iottalk/iottalk_server_1.0 && sudo -H pip3 install --upgrade requests


# Install uwsgi
RUN apt update
RUN apt install -y -qq libpcre3 libpcre3-dev
RUN pip3 install uwsgi

# Setup autorun iottalk daemon
#COPY iottalk.service /etc/systemd/system/iottalk.service
#RUN systemctl enable iottalk.service
#CMD ["/usr/sbin/init"]
#CMD ["/bin/systemctl", "start", "iottalk.service"]

EXPOSE 9999
EXPOSE 5566
EXPOSE 7788
EXPOSE 8000
EXPOSE 80

ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf
RUN sed -i '/#!\/usr\/bin\/python/c\#!/usr/bin/python2' /usr/bin/supervisord
ENTRYPOINT ["sh", "-c", "/usr/bin/supervisord"]
