FROM ubuntu:16.04

# Install.
RUN \
  apt-get update && \
  apt-get install -y build-essential uuid-runtime && \
  apt-get install -y software-properties-common && \
  apt-get install -y jq byobu curl git htop man unzip vim wget sudo apt-transport-https lsb-release gnupg && \
  apt-get install -y devscripts && \
  apt-get install -y  python3-configobj python3-oauthlib python3-jsonpatch python3-jinja2 python3-jsonschema debhelper dh-systemd python3-contextlib2 python3-nose python3-setuptools python3-coverage python3-httpretty python3-unittest2 python3-mock python3-yaml python3-requests

RUN curl -sL https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/microsoft.asc.gpg > /dev/null

RUN echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/azure-cli.list

RUN apt-get update && \
    apt-get install azure-cli
    
RUN wget https://aka.ms/downloadazcopy-v10-linux -O /tmp/azcopy.tar.gz && \
    tar xvfz /tmp/azcopy.tar.gz --directory /usr/bin --wildcards "*/azcopy" --strip-components=1

# Define default command.
CMD ["bash"]
