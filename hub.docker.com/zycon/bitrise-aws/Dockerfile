FROM bitriseio/docker-bitrise-base:latest

RUN apt-get remove -y awscli \
 && pip install awscli awsebcli --upgrade \
 && npm install -g apollo
