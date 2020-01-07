FROM node:8

RUN apt-get update -y
RUN apt-get install -y python-dev zip

RUN curl -O https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py
RUN pip install awscli --upgrade

RUN npm install -g gulp wrappy newman newman-reporter-htmlextra

ENTRYPOINT ["/bin/bash", "-c"]
