FROM centos:7
RUN rpm -Uvh https://yum.puppetlabs.com/puppetlabs-release-pc1-el-7.noarch.rpm
RUN yum -y install puppetserver-2.7.2

# Install openssl to generate hash for given password for puppet users
RUN yum -y install openssl-1.0.2k
RUN adduser -g puppet puppet

# Install puppet modules
#   sudo to manage sudo users
RUN /opt/puppetlabs/bin/puppet module install saz-sudo
#   simp-gdm to manage gdm/custom.conf for autologin
RUN /opt/puppetlabs/bin/puppet module install simp-gdm --version 7.0.3
#   puppetlabs-git to install git
RUN /opt/puppetlabs/bin/puppet module install puppetlabs-git --version 0.5.0

CMD while true; do sleep 1000; done
