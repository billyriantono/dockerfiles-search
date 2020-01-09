FROM amazonlinux

RUN curl --silent --location https://rpm.nodesource.com/setup_8.x | bash - \
  && yum -y update \
  && yum -y install nodejs findutils gcc-c++ make git openssh-client aws-cli which \
  && npm install -g n serverless \
  && n 8.10

VOLUME /root