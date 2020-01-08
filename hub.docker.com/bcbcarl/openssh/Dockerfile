FROM debian:wheezy
MAINTAINER Carl X. Su <bcbcarl@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

# The password is root
RUN \
  echo "root:root" | chpasswd && \
  mkdir /var/run/sshd

# Install OpenSSH server
RUN \
  apt-get update && \
  apt-get install -y openssh-server && \
  apt-get clean && rm -rf /var/lib/apt/lists/*

EXPOSE 22

ENTRYPOINT ["/usr/sbin/sshd"]
CMD ["-D"]