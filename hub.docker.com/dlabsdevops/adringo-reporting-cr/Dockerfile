FROM ubuntu:16.04

ARG DOCKERIZE_VERSION="v0.6.1"
ENV DOCKERIZE_VERSION=$DOCKERIZE_VERSION

# Install base tools
RUN apt-get update && apt-get install -y curl apt-transport-https python python-pip && \
apt-get clean && apt-get autoclean && apt-get autoremove

# Install AWS CLI
RUN pip install awscli

# Install Crystal-Lang
RUN curl -sSL https://dist.crystal-lang.org/apt/setup.sh | bash && \
curl -sL "https://keybase.io/crystal/pgp_keys.asc" | apt-key add - && \
echo "deb https://dist.crystal-lang.org/apt crystal main" | tee /etc/apt/sources.list.d/crystal.list && \
apt-get update && \
apt-get --yes install crystal libssl-dev libxml2-dev libyaml-dev libgmp-dev libreadline-dev && \
apt-get clean && apt-get autoclean && apt-get autoremove

# Install dockerize
RUN curl -L https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz -o dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz && \
tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz && rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz
