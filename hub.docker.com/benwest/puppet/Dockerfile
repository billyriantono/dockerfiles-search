FROM centos

# Install puppet-release and puppet-agent (4.9.4 currently)...
RUN rpm -Uvh https://yum.puppetlabs.com/puppetlabs-release-pc1-el-7.noarch.rpm && \
yum install -y puppet-agent

# Create a volume for saving production code (or mounting your own)
VOLUME /etc/puppetlabs/code/environments/production

# Set the working directory to the root of puppet code.
WORKDIR /etc/puppetlabs/code/environments/production

# Do a masterless puppet run.
CMD /opt/puppetlabs/bin/puppet apply .
