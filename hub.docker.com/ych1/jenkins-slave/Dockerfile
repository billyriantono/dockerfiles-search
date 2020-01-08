

FROM ubuntu:latest


# Make sure the package repository is up to date.
RUN apt-get update
RUN apt-get -y upgrade

# Install a basic SSH server
RUN apt-get install -y openssh-server openjdk-7-jdk
RUN sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd


# Jenkins user
RUN useradd -m -s /bin/bash jenkins && \
    echo jenkins:jenkins | chpasswd && \
    echo "jenkins ALL=(root) NOPASSWD: ALL" > /etc/sudoers.d/jenkins && \
    chmod 440 /etc/sudoers.d/jenkins && \
    mkdir -p /var/run/sshd



# Standard SSH port
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]