FROM jenkins/jenkins:2.200

USER root

RUN apt-get update \
    && apt-get -y install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    software-properties-common \
    && curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - \
    && add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable" \
   && apt-get update \
   && apt-cache madison docker-ce \
   && apt-get -y install docker-ce=5:19.03.3~3-0~debian-stretch docker-ce-cli=5:19.03.3~3-0~debian-stretch containerd.io