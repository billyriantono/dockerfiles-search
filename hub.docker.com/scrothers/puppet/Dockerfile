FROM layerworx/centos

ENV VERSION 3.7.1

RUN rpm --import https://yum.puppetlabs.com/RPM-GPG-KEY-puppetlabs && \
    rpm -ivh http://yum.puppetlabs.com/puppetlabs-release-el-6.noarch.rpm

RUN yum -y install facter hiera ruby ruby-augeas ruby-shadow \
    rubygem-json puppet-$VERSION && yum clean all
