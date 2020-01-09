FROM node:12.3.1-stretch

RUN apt-get update && apt-get install -y \
        apt-transport-https \
        ca-certificates \
        curl \
        gnupg2 \
        software-properties-common \
        zsh 

RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -

# lets install docker
RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"

RUN apt-get update && apt-get install -y \
        docker-ce \
        docker-ce-cli \
        containerd.io 

# Set the default shell to bash instead of sh
RUN sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"

# Docker compose as well!
RUN curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
RUN ["chmod", "+x", "/usr/local/bin/docker-compose"]

ENV SHELL /bin/zsh

