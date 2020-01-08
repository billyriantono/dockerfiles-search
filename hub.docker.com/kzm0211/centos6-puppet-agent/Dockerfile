From centos:6
MAINTAINER inamuu "https://github.com/kzm0211/"

RUN rpm -U http://yum.puppetlabs.com/puppetlabs-release-pc1-el-6.noarch.rpm \
    && yum -y -q install puppet-agent \
    && rm -f /etc/puppetlabs/puppet/hiera.yaml \
    && rpm -e puppetlabs-release-pc1 \
    ;\
    yum clean all

CMD ["/bin/bash"]
