FROM centos:7
MAINTAINER jonathan.dupuich@gmail.com

# Install repository
RUN rpm -ivh https://yum.puppetlabs.com/puppetlabs-release-el-7.noarch.rpm

# Install packages
RUN yum update -y && yum install -y \
	git \
	puppet \
	wget \
	&& yum clean -y all
	
RUN gem install puppet-lint
RUN puppet module install puppetlabs-concat 

WORKDIR /root
RUN mkdir /root/puppet

COPY entry.sh /root/entry.sh

RUN chmod +x entry.sh
ENTRYPOINT ["./entry.sh"]