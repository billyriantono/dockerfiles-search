FROM ubuntu:16.04

COPY Dockerfile /

ARG BUILD_DATE
ARG VCS_REF
ARG VERSION

ENV PUPPET_AGENT_VERSION="1.8.0" UBUNTU_CODENAME="xenial"

LABEL org.label-schema.build-date=$BUILD_DATE \
			org.label-schema.name="puppet-agent-ubuntu" \
			org.label-schema.description="Puppet agent ubuntu" \
			org.label-schema.url="http://andradaprieto.es" \
			org.label-schema.vcs-ref=$VCS_REF \
			org.label-schema.vcs-url="https://github.com/jandradap/puppet-agent-ubuntu" \
			org.label-schema.vendor="Jorge Andrada Prieto" \
			org.label-schema.version=$PUPPET_AGENT_VERSION \
			org.label-schema.schema-version="1.0" \
			maintainer="Jorge Andrada Prieto <jandradap@gmail.com>" \
			org.label-schema.docker.cmd="docker run --rm -h 'test01' --add-host='puppetServer.dom puppet:IP_puppetServer' jorgeandrada/puppet-agent-ubuntu &"

RUN apt-get update && \
    apt-get install --no-install-recommends -y wget ca-certificates lsb-release && \
    wget https://apt.puppetlabs.com/puppetlabs-release-pc1-"$UBUNTU_CODENAME".deb && \
    dpkg -i puppetlabs-release-pc1-"$UBUNTU_CODENAME".deb && \
    rm puppetlabs-release-pc1-"$UBUNTU_CODENAME".deb && \
    apt-get update && \
    apt-get install --no-install-recommends -y puppet-agent="$PUPPET_AGENT_VERSION"-1"$UBUNTU_CODENAME" && \
    apt-get remove --purge -y lsb-release wget && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ENV PATH=/opt/puppetlabs/server/bin:/opt/puppetlabs/puppet/bin:/opt/puppetlabs/bin:$PATH

COPY entrypoint.sh /root

ENTRYPOINT ["/root/entrypoint.sh"]
