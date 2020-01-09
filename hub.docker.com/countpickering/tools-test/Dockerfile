#Tools Container
#Install using CentOS7
FROM centos:centos7
#Update and intell epel repo and some tools
RUN yum -y install epel-release && \
    yum -y install wget git
#Download Yarn repo    
RUN wget https://dl.yarnpkg.com/rpm/yarn.repo -O /etc/yum.repos.d/yarn.repo
#Install yarn and cleanup
RUN yum install yarn -y && \
    yum -y clean all
#configure NodeSource repository
RUN curl --silent --location https://rpm.nodesource.com/setup_6.x | bash -
#Install yarn tools
RUN yarn global add eslint@3.19.0 && \
    yarn global add gulp-cli && \
    yarn global add karma-cli
CMD tail -f /dev/null
