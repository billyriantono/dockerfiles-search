FROM google/cloud-sdk
MAINTAINER Peter Wiggers <peter@bitlayer.nl>

ENV SOPS_VERSION=3.0.4
ENV KUBEVAL_VERSION=0.7.3

# install pip
RUN apt-get update && apt-get install -y python-pip git

# install nodejs and knexjs (SQL ORM)
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get install -y nodejs build-essential
RUN npm install -g knex

# install sops
RUN curl -LO https://github.com/mozilla/sops/releases/download/${SOPS_VERSION}/sops_${SOPS_VERSION}_amd64.deb && \
    dpkg -i sops_${SOPS_VERSION}_amd64.deb

# install kubeval
RUN curl -LO https://github.com/garethr/kubeval/releases/download/${KUBEVAL_VERSION}/kubeval-linux-amd64.tar.gz && \
    tar -xzvf kubeval-linux-amd64.tar.gz && \
    mv kubeval /usr/local/bin

# install requirements
COPY requirements.txt /tmp
RUN pip install --no-cache-dir -r /tmp/requirements.txt
