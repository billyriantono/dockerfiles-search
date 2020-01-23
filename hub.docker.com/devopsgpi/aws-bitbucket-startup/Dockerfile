# Python is used to form the base of image. No need to intall pip or python
FROM python:buster

LABEL author="Myrtyl Santos for GPI" \
  email="myrtyl.santos@gpi.id"

# Install Node and NPM 
RUN \
  echo "deb https://deb.nodesource.com/node_12.x buster main" > /etc/apt/sources.list.d/nodesource.list && \
  wget -qO- https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add - && \
  apt-get update && \
  apt-get install -yqq nodejs

# Install AWS Cli 
RUN \
  pip install awscli

# Remove redundant folders
RUN rm -rf /var/lib/apt/lists/*
