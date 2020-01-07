#Dockerfile for java golang environment
FROM base/archlinux:latest
MAINTAINER	WangLei	"leith.wong@gmail.com"

# Change mirrorlist and add yaourt repository to pacman.conf
RUN sed -i -e '1i Server = http://mirrors.163.com/archlinux/$repo/os/$arch' /etc/pacman.d/mirrorlist
#RUN echo "\n[archlinuxfr]\nSigLevel = Never\nServer = http://repo.archlinux.fr/\$arch" >> /etc/pacman.conf
RUN echo "[archlinuxfr]" >> /etc/pacman.conf; echo "SigLevel = Never" >> /etc/pacman.conf;echo "Server = http://repo.archlinux.fr/\$arch" >> /etc/pacman.conf

RUN	pacman-key --init
RUN pacman-key --populate archlinux

# Update to newest
RUN pacman -Syu --noconfirm 

# Upgrade pacman db version
RUN pacman-db-upgrade

# Install git jdk and golang
RUN pacman -S yaourt git jdk7-openjdk go --noconfirm

# Add java&golang ENV
ENV PATH /usr/src/go/bin:$PATH

RUN mkdir -p /go/src
ENV GOPATH /go
ENV PATH /go/bin:$PATH
WORKDIR /go

ENV PATH $PATH:/opt/java/bin
ENV JAVA_HOME /opt/java

# Clean package cache
RUN echo "y" | pacman -Scc 
