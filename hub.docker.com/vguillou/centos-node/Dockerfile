FROM vguillou/centos-sshpass:7.7

RUN curl -sL https://rpm.nodesource.com/setup_10.x | bash - \
 && yum -y update \
 && yum -y install gcc-c++ make nodejs-10.16.3 git \
 && yum clean all \
 && rm -rf /var/cache/yum \
 && curl -o- -L https://yarnpkg.com/install.sh | bash

ENV PATH="/root/.yarn/bin:${PATH}"
