FROM node:6.1
#RUN curl -L https://get.docker.com/builds/Linux/x86_64/docker-1.10.3.tgz | tar xvz && cp docker/docker /usr/local/bin && rm -rf docker
RUN cd / &&  curl -L https://get.docker.com/builds/Linux/x86_64/docker-1.10.3.tgz | tar xvz
RUN curl -L https://github.com/docker/compose/releases/download/1.7.0/docker-compose-Linux-x86_64 > /usr/local/bin/docker-compose && chmod +x /usr/local/bin/docker-compose
RUN curl -L https://github.com/docker/machine/releases/download/v0.6.0/docker-machine-Linux-x86_64 > /usr/local/bin/docker-machine && chmod +x /usr/local/bin/docker-machine
RUN apt-get update && apt-get install -y jq curl 
