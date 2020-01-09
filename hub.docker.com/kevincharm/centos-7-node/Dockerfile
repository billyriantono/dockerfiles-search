FROM centos:7

RUN yum groupinstall -y 'Development Tools'

# node & npm
RUN curl -sL https://rpm.nodesource.com/setup_12.x | bash - && \
    yum install -y nodejs && \
    node --version && \
    npm --version

# yarn
RUN curl -sL https://dl.yarnpkg.com/rpm/yarn.repo | tee /etc/yum.repos.d/yarn.repo && \
    yum install -y yarn && \
    yarn --version
