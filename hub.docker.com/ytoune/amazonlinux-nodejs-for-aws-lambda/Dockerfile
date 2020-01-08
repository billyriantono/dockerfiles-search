FROM amazonlinux:latest

RUN curl -sL https://rpm.nodesource.com/setup_8.x | bash && \
  yum install -y awscli git zip nodejs && \
  npm i -g yarn
