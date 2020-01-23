FROM ubuntu:trusty
MAINTAINER Abhishek Jaiswal <abhishekjaiswal.kol@gmail.com>

# Prevent dpkg errors
ENV TERM=xterm-256color

# Set mirrors to india
# RUN sed -i "s/http:\/\/archive./http:\/\/in.archive./g" /etc/apt/sources.list

# Install Python runtime , It will not install recomennded or suggested packages
RUN apt-get update && \
    apt-get install -qy \
    -o APT::Install-Recommend=false -o APT::Install-Suggests=false \
    python python-virtualenv libpython2.7 python-mysqldb

# Create virtual environment
# why virtual env in docker read this:  https://hynek.me/articles/virtualenv-lives/

# Upgrade PIP in virtual environment to latest version
# docker run in bourne shell so source is not used instead use . operator

RUN virtualenv /appenv && \
    . /appenv/bin/activate && \
    pip install pip --upgrade

# Add entrypoint script
ADD scripts/entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]

LABEL application=todobackend