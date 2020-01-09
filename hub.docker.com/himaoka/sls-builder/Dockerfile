FROM python:3.7-stretch

RUN /bin/sh -c 'curl -sL https://deb.nodesource.com/setup_8.x | bash -'
RUN /bin/sh -c 'apt update; apt install -y nodejs build-essential'
RUN npm install -g serverless
