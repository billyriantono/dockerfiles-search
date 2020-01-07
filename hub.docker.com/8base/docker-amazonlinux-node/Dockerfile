FROM amazonlinux:2

RUN curl -sL https://rpm.nodesource.com/setup_8.x | bash - \
  && yum -y update \
  && yum -y install nodejs findutils gcc-c++ make git openssh-client aws-cli which \
  && npm install -g npm@6.4.1
  
RUN curl --silent --location https://dl.yarnpkg.com/rpm/yarn.repo | tee /etc/yum.repos.d/yarn.repo \
  && yum -y install yarn-1.10.1

EXPOSE 3000

CMD ["node"]
