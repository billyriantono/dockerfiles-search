FROM ubuntu:trusty
MAINTAINER Vikas Kumar <vikas@reachvikas.com>

# Prevent dpkg errors
ENV TERM=xterm-256color

# Set mirrors to NZ  (speed package installation time)
RUN sed -i "s/http:\/\/archive./http:\/\/nz.archive./g" /etc/apt/sources.list

# Install Python runtime (install only what is required, not recommended ones)
RUN apt-get update && \
    apt-get install -qy \
    -o APT::Install-Recommend=false -o APT::Install-Suggests=false \
    python python-virtualenv libpython2.7 python-mysqldb

# Create virtual environment (we need to use '.' and not source as docker image used /bin/sh and not /bin/bash)
# Upgrade PIP in virtual environment to latest version
RUN virtualenv /appenv && \
    . /appenv/bin/activate && \
    pip install pip --upgrade

# Add entrypoint script
ADD scripts/entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]

LABEL application=todobackend
