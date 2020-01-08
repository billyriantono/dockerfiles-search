FROM ubuntu:trusty
MAINTAINER Jordan Starcher <jstarcher@gmail.com>

RUN apt-get update && \
    apt-get install -y \
            git \
            openjdk-7-jdk \
            openssh-server && \
    apt-get clean

# Configure ssh and jenkins user
RUN sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd && \
    mkdir -p /var/run/sshd && \
    adduser --quiet jenkins && \
    echo "jenkins:jenkins" | chpasswd && \
    echo "jenkins   ALL=(ALL)       NOPASSWD: ALL" >> /etc/sudoers.d/jenkins && \
    sed -ri 's/Defaults    requiretty/#Defaults    requiretty/g' /etc/sudoers

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]

