FROM google/cloud-sdk:slim
MAINTAINER "amanoyu" <alterna_cloud@me.com>

RUN \
     apt-get -y install \
     apt-transport-https \
     ca-certificates \
     curl \
     gnupg2 \
     software-properties-common &&\
     curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -  &&\
     add-apt-repository \
     "deb [arch=amd64] https://download.docker.com/linux/debian \
     $(lsb_release -cs) \
     stable"  &&\
     apt-get -y update &&\
     apt-get -y install kubectl &&\
     apt-get -y install docker-ce &&\
     pip install docker-compose
