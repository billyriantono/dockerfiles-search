FROM ubuntu:bionic
LABEL maintainer="erathorus@gmail.com"

# Install essential tools
RUN apt-get update && apt-get install -y --no-install-recommends \
		ca-certificates \
		curl \
		wget \
        git

# Force Docker to use UTF-8 encodings
ENV LANG en_US.UTF-8

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
