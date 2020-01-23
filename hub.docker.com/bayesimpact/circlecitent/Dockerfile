FROM java:8-jdk
MAINTAINER Baptiste Mathus <batmat@batmat.net>

RUN apt-get update -y && \
    apt-get -y upgrade && \
    apt-get install -y \
                        git \
                        subversion \
                        openjdk-8-jdk \
                        openssh-server && \
    apt-get clean

# Configure the SSH server
RUN sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd
RUN mkdir -p /var/run/sshd

# Add user jenkins/jenkins to the image
RUN adduser --quiet jenkins
RUN echo "jenkins:jenkins" | chpasswd

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
