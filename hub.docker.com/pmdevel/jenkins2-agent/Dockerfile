FROM openjdk:8-jdk

ARG USER_HOME_DIR="/var/jenkins-agent"

RUN apt-get update && apt-get install -y git curl ssh && rm -rf /var/lib/apt/lists/*

# Set user jenkins to the image
RUN useradd -m -d /var/jenkins-agent -s /bin/sh jenkins &&\
    echo "jenkins:jenkins" | chpasswd

# SSH stuff
RUN mkdir /var/run/sshd && chmod 0755 /var/run/sshd

# Standard SSH port
EXPOSE 22

# Default command
CMD ["/usr/sbin/sshd", "-D"]
