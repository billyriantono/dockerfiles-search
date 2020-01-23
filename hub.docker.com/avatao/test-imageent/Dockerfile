FROM ubuntu:16.04

ENV PUPPET_AGENT_VERSION="1.8.1" R10K_VERSION="2.2.2" CODENAME="xenial" 

WORKDIR /

RUN apt-get update && \
    apt-get install --no-install-recommends -y lsb-release wget ca-certificates && \
    wget https://apt.puppetlabs.com/puppetlabs-release-pc1-"$CODENAME".deb && \
    dpkg -i puppetlabs-release-pc1-"$CODENAME".deb && \
    rm puppetlabs-release-pc1-"$CODENAME".deb && \
    apt-get update && \
    apt-get install --no-install-recommends -y puppet-agent="$PUPPET_AGENT_VERSION"-1"$CODENAME" && \
    apt-get remove --purge -y wget ca-certificates && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* 

RUN apt-get update && \
    apt-get install --no-install-recommends -y git-core && \
    /opt/puppetlabs/puppet/bin/gem install r10k:"$R10K_VERSION" --no-ri --no-rdoc && \
    apt-get remove --purge -y git-core && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* 

COPY Puppetfile /Puppetfile
RUN /opt/puppetlabs/puppet/bin/r10k puppetfile install --moduledir /etc/puppetlabs/code/modules

COPY manifests /manifests

COPY hiera.yaml /hiera.yaml
COPY hieradata /hieradata

  
    
RUN apt-get update && \
    FACTER_hostname=aim /opt/puppetlabs/bin/puppet apply manifests/init.pp --verbose --show_diff --summarize --hiera_config=/hiera.yaml --app_management && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* 
    
  

LABEL com.puppet.inventory="/inventory.json"
RUN /opt/puppetlabs/bin/puppet module install puppetlabs-inventory && \
    /opt/puppetlabs/bin/puppet inventory all > /inventory.json

EXPOSE 8080

CMD ["/usr/local/tomcat/bin/catalina.sh", "run"]
