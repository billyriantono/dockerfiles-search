FROM centos:7
RUN cat /etc/redhat-release


# Install nodejs
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | gpg --import \
    && curl --silent --location https://rpm.nodesource.com/setup_10.x | bash - \
    && curl --silent --location https://dl.yarnpkg.com/rpm/yarn.repo > /etc/yum.repos.d/yarn.repo \
    && yum update -y \
    && yum -y install nodejs git vim yarn gcc-c++ make
