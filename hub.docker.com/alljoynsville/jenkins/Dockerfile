FROM jenkins/jenkins:lts
USER root
RUN apt-get update -yqq && \
    apt-get install -yqq sudo apt-transport-https binutils  \
                         vim less rsync && \
    curl -fsSL get.docker.com | sudo bash && \
    usermod -aG docker jenkins && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
