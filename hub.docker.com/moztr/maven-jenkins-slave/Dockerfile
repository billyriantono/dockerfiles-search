FROM debian:jessie
MAINTAINER mark<mark.oliver.schmitt@gmail.com>

RUN echo "deb http://ftp.debian.org/debian jessie-backports main" >> /etc/apt/sources.list

# openssh for jenkins, openjre for jenkins slave. this prevents the jenkins setup to download this every time
RUN apt-get update && apt-get install -y maven openssh-server openjdk-8-jdk-headless && apt-get clean

RUN useradd -m -d /home/jenkins -s /bin/sh jenkins &&\
  echo "jenkins:jenkins" | chpasswd

EXPOSE 22

RUN mkdir /var/run/sshd

CMD ["/usr/sbin/sshd", "-D"]
