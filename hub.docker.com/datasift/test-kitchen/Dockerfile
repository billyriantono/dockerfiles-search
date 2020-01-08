FROM centos:7

# Install iproute so kitchen-nodes will detect the ip correctly
RUN yum install iproute -y

# Install service
RUN yum -y install initscripts

# Install the Chef client
RUN curl -O https://packages.chef.io/files/stable/chef/12.17.44/el/7/chef-12.17.44-1.el7.x86_64.rpm && \
    rpm -i chef-12.17.44-1.el7.x86_64.rpm && \
    rm chef-12.17.44-1.el7.x86_64.rpm

# Prepare the gem cache used by Kitchen and Busser
RUN GEM_HOME=/tmp/verifier/gems \
    GEM_PATH=/tmp/verifier/gems \
    GEM_CACHE=/tmp/verifier/gems/cache \
    /opt/chef/embedded/bin/gem install \
        --no-rdoc --no-ri --no-format-executable \
        --bindir /tmp/verifier/bin --no-user-install \
        bundler \
        rspec:3.5.0 \
        rspec-core:3.5.4 \
        rspec-expectations:3.5.0 \
        rspec-its:1.2.0 \
        rspec-mocks:3.5.0 \
        rspec-support:3.5.0 \
        serverspec:2.37.2 \
        serverspec_extensions:0.0.2 \
        busser \
        busser-bash \
        busser-serverspec \
        thor \
        yarjuf && \
    useradd -m -s /bin/bash -p '*' kitchen && \
    chown -R kitchen:kitchen /tmp/verifier

RUN echo $'NETWORKING=yes\n\
HOSTNAME=localhost.localdomain' > /etc/sysconfig/network
