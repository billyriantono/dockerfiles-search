FROM centos:7
# or RHEL...

# Sourced and based on https://github.com/hashicorp/docker-consul/blob/master/0.X/Dockerfile
# Consul - https://releases.hashicorp.com/consul/1.0.3/consul_1.0.3_linux_amd64.zip?_ga=2.241983494.522517661.1517849930-558920476.1516803903
# Docs - https://www.consul.io/intro/index.html

MAINTAINER DonaldSimpson@gmail.com

# This is the release of Consul to pull in.
ENV CONSUL_VERSION=1.0.6

# Create a consul user and group first so the IDs get set the same way, even as
# the rest of this may change over time.
RUN groupadd consul && \
    useradd -g consul consul

USER root

# Set up certificates, base tools, and Consul.
RUN mkdir -p /tmp/build
ADD https://releases.hashicorp.com/consul/1.0.6/consul_${CONSUL_VERSION}_linux_amd64.zip /tmp/build/consul_${CONSUL_VERSION}_linux_amd64.zip


RUN yum install -y ca-certificates curl gnupg libcap openssl unzip which && \
    cd /tmp/build && \
    unzip -d /bin consul_${CONSUL_VERSION}_linux_amd64.zip && \
    cp /bin/consul /usr/local/bin/consul && \
    cd /tmp && \
    rm -rf /tmp/build

# Fetch and chmod dumb-init from artifactory
ADD https://github.com/Yelp/dumb-init/releases/download/v1.2.1/dumb-init_1.2.1_amd64 /usr/local/bin/dumb-init
RUN chmod ugo+rx /usr/local/bin/dumb-init

# The /consul/data dir is used by Consul to store state. The agent will be started
# with /consul/config as the configuration directory so you can add additional
# config files in that location.
RUN mkdir -p /consul/data && \
    mkdir -p /consul/config && \
    chown -R consul:consul /consul

# Expose the consul data directory as a volume since there's mutable state in there.
VOLUME /consul/data

# Consul doesn't need root privileges so we run it as the consul user from the
# entry point script. The entry point script also uses dumb-init as the top-level
# process to reap any zombie processes created by Consul sub-processes.
COPY docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh

RUN chmod a+x /usr/local/bin/consul /usr/local/bin/docker-entrypoint.sh /bin/consul

RUN consul version && \
    which consul && \
    which docker-entrypoint.sh &&\
    id consul

# Server RPC is used for communication between Consul clients and servers for internal
# request forwarding.
EXPOSE 8300

# Serf LAN and WAN (WAN is used only by Consul servers) are used for gossip between
# Consul agents. LAN is within the datacenter and WAN is between just the Consul
# servers in all datacenters.
EXPOSE 8301 8301/udp 8302 8302/udp

# HTTP and DNS (both TCP and UDP) are the primary interfaces that applications
# use to interact with Consul.
EXPOSE 8500 8600 8600/udp

USER root

ENTRYPOINT ["docker-entrypoint.sh"]

#CMD exec /bin/bash -c "trap : TERM INT; sleep infinity & wait"

# By default you'll get an insecure single-node development server that stores
# everything in RAM, exposes a web UI and HTTP endpoints, and bootstraps itself.
# Don't use this configuration for production.
CMD ["agent", "-dev", "-client", "0.0.0.0"]
