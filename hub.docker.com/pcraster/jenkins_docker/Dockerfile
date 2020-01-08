FROM pcraster/jenkins_base:latest

MAINTAINER Kor de Jong <k.dejong1@uu.nl>

# Add Docker engine and Docker compose to the image.
USER root
RUN \
    curl -fsSL https://yum.dockerproject.org/gpg | sudo apt-key add - && \
    sudo add-apt-repository "deb https://apt.dockerproject.org/repo \
        debian-$(lsb_release -cs) main" && \
    apt-get update && \
    apt-get install -y docker-engine=1.13.0-0~debian-jessie && \
    rm -fr /var/lib/apt/lists/* && \
    curl -L https://github.com/docker/compose/releases/download/1.10.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose && \
    chmod +x /usr/local/bin/docker-compose

# List availabel versions of Docker:
# apt-cache madison docker-engine
