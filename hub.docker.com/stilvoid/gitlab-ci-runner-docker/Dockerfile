FROM ubuntu:14.04
MAINTAINER Stilvoid <steve@offend.me.uk>

ENV DEBIAN_FRONTEND=noninteractive

# Install requirements
RUN apt-get -q update \
    && apt-get install -q -y \
    curl \
    wget \
    && apt-get -q -y autoremove \
    && apt-get -q -y autoclean

# Add gitlab-runner user
RUN useradd -m -r gitlab-runner

# Install gitlab-runner
RUN wget -q https://s3-eu-west-1.amazonaws.com/downloads-packages/ubuntu-14.04/gitlab-runner_5.1.0~pre.omnibus.1-1_amd64.deb \
    && dpkg -i gitlab-runner_5.1.0~pre.omnibus.1-1_amd64.deb \
    && apt-get autoclean \
    && rm gitlab-runner_5.1.0~pre.omnibus.1-1_amd64.deb

# Install job dependencies
RUN apt-get -q update \
    && apt-get install -q -y \
    docker.io \
    git \
    && apt-get -q -y autoremove \
    && apt-get -q -y autoclean

ADD entrypoint.sh /

ENV HOME /home/gitlab-runner

ENTRYPOINT ["/bin/bash", "-l", "entrypoint.sh"]
