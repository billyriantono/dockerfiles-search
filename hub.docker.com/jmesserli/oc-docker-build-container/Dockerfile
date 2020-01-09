FROM jmesserli/openjdk-with-docker

ENV OCTOPUS_VERSION 4.30.0

# Install CoreCLR dependencies for Octopus CLI
RUN apt-get update && apt-get -y install libunwind8 && \
        apt-get clean && rm -rf /var/lib/apt/lists/*

RUN mkdir /opt/octo && cd /opt/octo && \
    curl -so octo.tar.gz https://download.octopusdeploy.com/octopus-tools/$OCTOPUS_VERSION/OctopusTools.$OCTOPUS_VERSION.debian.8-x64.tar.gz && \
    tar -xvf octo.tar.gz && rm -f octo.tar.gz
