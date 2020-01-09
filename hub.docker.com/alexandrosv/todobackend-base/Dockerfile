# All operating system dependencies should be resolved in this image
FROM ubuntu:trusty
MAINTAINER Alejandro Villamarin <favm@emaiil.com>

# Suppress dpkg errors
ENV TERM=xterm-256color

# Set mirrors to CZ
RUN sed -i "s/https:\/\/archive./https:\/\/cz.archive./g" /etc/apt/sources.list

# Install Python
RUN apt-get update && \
    apt-get install -y \
    -o APT::Install-Recommend=false -o APT::Install-Suggest=false \
     python python-virtualenv libpython2.7 python-mysqldb

# Create virtual environment and upgrade PIP
# https://hynek.me/articles/virtualenv-lives/
RUN virtualenv /appenv && \
    . /appenv/bin/activate && \
    pip install pip --upgrade

# Add entrypoint script
ADD scripts/entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]

LABEL application=todobackend