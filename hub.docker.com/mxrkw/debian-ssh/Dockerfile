FROM debian:latest

LABEL maintainer="Mxrk <github.com/mxrk>"

RUN apt-get update -y && apt-get upgrade -y && apt-get install -y \
  openssh-server \
  nano \
  && rm -rf /var/lib/apt/lists/*

RUN echo 'root:password' | chpasswd

RUN mkdir /var/run/sshd

RUN sed 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' -i /etc/ssh/sshd_config

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]