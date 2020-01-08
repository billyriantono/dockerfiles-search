FROM ubuntu:16.04

# Install tools
RUN apt-get update \
  && apt-get install -y wget curl apt-transport-https git vim python3 python3-pip \
  && rm -rf /var/lib/apt/lists/*

# Install OpenStack CLI
RUN pip3 install python-openstackclient python-neutronclient python-novaclient python-swiftclient python-cinderclient python-glanceclient

# Install Cloud Foundry CLI
RUN wget -q -O - https://packages.cloudfoundry.org/debian/cli.cloudfoundry.org.key | apt-key add - \
    && echo "deb http://packages.cloudfoundry.org/debian stable main" | tee /etc/apt/sources.list.d/cloudfoundry-cli.list \
    && apt-get update \
    && apt-get install -y cf-cli \
    && rm -rf /var/lib/apt/lists/*

ENV HOME /root
WORKDIR $HOME
