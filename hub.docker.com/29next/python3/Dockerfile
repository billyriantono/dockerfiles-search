FROM ubuntu:18.04

MAINTAINER 29Next

# Prevent dpkg errors
ENV TERM=xterm-256color
# Set noninteractive for installing package
ARG DEBIAN_FRONTEND=noninteractive

# Install Package
RUN apt-get update && \
    apt-get install -qy \
    #python 3
    python3.6 python3.6-dev python3-pip python3-venv \
    # pillow dependency
    libtiff5-dev libjpeg8-dev zlib1g-dev libjpeg-dev \
    libfreetype6-dev liblcms2-dev libwebp-dev libharfbuzz-dev libfribidi-dev \
    tcl8.6-dev tk8.6-dev python-tk \
    # M2Crypto dependency
    build-essential libssl-dev libxml2 libxslt-dev swig \
    # postgres dependency
    libpq-dev \
    # others
    gettext git vim locales

# set locale to can decode unicode
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8
ENV LC_ALL en_US.UTF-8

# Create virtual environment
# Upgrade PIP in virtual environment to latest version
RUN python3 -m venv /appenv && \
    . /appenv/bin/activate && \
       pip install --upgrade pip && \
       pip install setuptools wheel

# Add entrypoint script
ADD scripts/entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]

