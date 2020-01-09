FROM python:2.7.11

MAINTAINER Kevin Delfour <kevin@sogilis.com>

# Install pre-requisite
# Make sure the package repository is up to date.
RUN dpkg --add-architecture i386
RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get install -y cppcheck openssh-server curl git libc6:i386 libncurses5:i386 libstdc++6:i386

# Install a basic SSH server
RUN sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd
RUN mkdir -p /var/run/sshd

# Install JDK 7 (latest edition)
RUN apt-get install -y openjdk-7-jdk

# Add user jenkins to the image
RUN adduser --quiet jenkins
# Set password for the jenkins user (you may want to alter this).
RUN echo "jenkins:jenkins" | chpasswd

# Install PlatformIO
RUN python -c "$(curl -fsSL https://raw.githubusercontent.com/platformio/platformio/master/scripts/get-platformio.py)"

# Prepare workspace volume
RUN mkdir -p /usr/local/workspace
VOLUME /usr/local/workspace

# Positionning in worspace
WORKDIR /usr/local/workspace
COPY testCode /usr/local/workspace/testCode

RUN cd /usr/local/workspace/testCode && platformio run
# Standard SSH port
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
