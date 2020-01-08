FROM ubuntu:18.04

# Install Packages
RUN apt-get update && apt-get install -y \
    curl \
    git \
    gnupg \
    rsync \
    ssh

# Install Nodejs 10.x LTS
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - \
    && apt-get install -y nodejs

# Clean-up
RUN apt-get remove -y \
    curl \
    gnupg \
    && rm -rf /var/lib/apt/lists/*

