FROM google/cloud-sdk:latest
MAINTAINER Us Media <info@usmedia.nl>

#
# Install dependencies
#
RUN apt-get update \
&& apt-get install -y \
    gettext-base

#
# Cleanup
#
RUN rm -rf /var/lib/apt/lists/*

