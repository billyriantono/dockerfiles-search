FROM jenkinsci/slave:3.10-1

USER root

RUN apt-get update \
  && apt-get upgrade -y \
  && apt-get install -y \
    sudo \
    libltdl-dev \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common \
  && rm -rf /var/lib/apt/lists/*

RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers

USER jenkins
