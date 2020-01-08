FROM node:7.8.0-wheezy

RUN npm install -g @angular/cli
RUN apt-get update
RUN apt-get -y install python-pip
RUN apt-get -y install python-dev
RUN pip install --upgrade --user awscli
ENV PATH="~/.local/bin:${PATH}"