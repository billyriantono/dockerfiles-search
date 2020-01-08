FROM ubuntu:14.04


MAINTAINER joaniznardo (github)

RUN apt-get update && apt-get install -y curl debconf-utils dnsutils inotify-tools openssh-server sudo supervisor tcpdump traceroute && mkdir -p /var/run/sshd && useradd -m ubuntu && echo "ubuntu:ubuntu" | chpasswd && adduser ubuntu sudo 

COPY supervisor-sshd.conf /etc/supervisor/conf.d

CMD  supervisord -nc /etc/supervisor/supervisord.conf

