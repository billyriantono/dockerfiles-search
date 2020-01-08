FROM davidzlewis/base

RUN rpm --import https://yum.puppetlabs.com/RPM-GPG-KEY-puppetlabs && \
    rpm -Uvh https://yum.puppetlabs.com/puppetlabs-release-pc1-el-7.noarch.rpm

RUN yum install yum-utils -y && yum-config-manager --enable centosplus >& /dev/null && yum clean all

ENV PUPPET_VERSION 2.3.2

RUN yum install -y puppetserver-$PUPPET_VERSION \
    && yum clean all
    
ADD puppet.conf /etc/puppet/puppet.conf

VOLUME ["/opt/puppet"]

EXPOSE 8140

ENTRYPOINT [ "/usr/bin/puppet", "master", "--no-daemonize", "--verbose" ]
