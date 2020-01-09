FROM fedora:23
MAINTAINER Katsuyuki Tateishi <kt@wheel.jp>

RUN dnf update -y && \
    dnf install -y openssh-server nmap-ncat && \
    dnf group install -y 'Development Tools' && \
    dnf clean all

ADD docker-entry.sh /

CMD ["/docker-entry.sh"]
