From debian

LABEL Maintainer="Wanderson Pereira <wanderson.coord@gmail.com>"

# Install Dependences
RUN apt-get update \
 -qq && apt-get install -y -qq apt-transport-https \
 ca-certificates \
 gnupg-agent  \
 build-essential \
 software-properties-common \
 libssl-dev \
 libffi-dev \
 python3-dev \
 unixodbc-dev \
 curl \
 python3-pip

# Install Docker
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN apt-key fingerprint 0EBFCD88
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"

RUN apt-get update \
 && apt-get -y install docker-ce \
 docker-ce-cli \
 containerd.io

# Install awscli
RUN export PATH=/usr/local/bin:$PATH
RUN pip3 install awscli --upgrade

RUN aws --version

EXPOSE 2375

CMD ["service", "docker", "start"]