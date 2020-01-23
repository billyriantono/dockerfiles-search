FROM amd64/debian:latest

MAINTAINER Emil Moe

ENV DEBIAN_FRONTEND noninteractive

WORKDIR /tmp

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y schroot debootstrap openssh-server inotify-tools

RUN adduser backup-user --disabled-password
RUN echo "backup-user:password" | chpasswd
RUN mkdir -p /var/backup

RUN echo "Match User backup" >> /etc/ssh/sshd_config
RUN echo "        ChrootDirectory /var/backup" >> /etc/ssh/sshd_config
RUN echo "        AllowTcpForwarding no" >> /etc/ssh/sshd_config

RUN sed -i 's/\/usr\/lib\/openssh\/sftp-server/internal-sftp/g' /etc/ssh/sshd_config

RUN echo "" > /empty.log

EXPOSE 22

ENTRYPOINT tail -f /empty.log
