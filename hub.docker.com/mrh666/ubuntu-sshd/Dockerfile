FROM ubuntu:14.04
MAINTAINER Andrey Kanevsky andrey@devops.co.il

RUN apt-get -yq update && \
    apt-get -yq install openssh-server && \
    mkdir -p /root/.ssh && \
    chmod 0700 /root/.ssh && \
    mkdir /var/run/sshd && \
    chmod 0755 /var/run/sshd

RUN sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config

COPY motd /etc/motd

COPY ssh-key.pub /root/.ssh/authorized_keys

RUN chmod 0640 /root/.ssh/authorized_keys

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
