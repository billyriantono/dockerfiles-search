FROM ubuntu:xenial

# install insecure vagrant ssh public key
COPY vagrant.pub /root/.ssh/authorized_keys

# based on https://docs.docker.com/engine/examples/running_ssh_service/
RUN apt-get update -qq && \
    apt-get install -yqq \
      ssh sudo vim && \
    rm -rf /var/lib/apt/lists/* && \
    chmod 700 /root/.ssh/ && \
    mkdir -p /var/run/sshd && \
    echo 'root:vagrant' | chpasswd && \
    sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed -i 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' /etc/pam.d/sshd

WORKDIR /root

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
