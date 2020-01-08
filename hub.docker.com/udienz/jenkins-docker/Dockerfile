# This Dockerfile is used to build an image containing basic stuff to be used as a Jenkins slave build node.
FROM udienz/buildpack:trusty
MAINTAINER mahyuddin susanto <udienz@gmail.com>


# Install and configure a basic SSH server
RUN apt-get update &&\
    apt-get install -y openssh-server git subversion bzr mercurial cvs sudo ruby ruby-dev build-essential &&\
    apt-get clean -y && rm -rf /var/lib/apt/lists/* &&\
    sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd &&\
    mkdir -p /var/run/sshd

# Install JDK 7 (latest edition)
RUN apt-get update &&\
    apt-get install -y --no-install-recommends default-jdk &&\
    apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Set user jenkins to the image
RUN adduser --quiet --disabled-password --gecos '' jenkins \
    && echo "jenkins:jenkins" | chpasswd \
    && echo 'jenkins ALL=NOPASSWD: ALL' > /etc/sudoers.d/jenkins

# Standard SSH port
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
