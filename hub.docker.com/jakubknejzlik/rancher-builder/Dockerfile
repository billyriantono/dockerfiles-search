FROM ubuntu

RUN apt-get update

RUN apt-get -y install python-pip git nodejs npm

RUN ln -s /usr/bin/nodejs /usr/bin/node

RUN pip install rancher-gitlab-deploy

RUN curl -fsSL https://get.docker.com/ | sh
