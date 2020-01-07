#
# Python Dockerfile
#
# https://github.com/umeice/python
#

# Pull base image.
FROM dockerfile/ubuntu

MAINTAINER @bungoume <bungoume@gmail.com>

# Install Python.
RUN \
  apt-get update && apt-get upgrade -y && \
  apt-get install -y python python-dev libxml2-dev libxslt-dev zlib1g-dev \
      libtiff4-dev libjpeg8-dev zlib1g-dev libfreetype6-dev liblcms2-dev \
      libwebp-dev tcl8.5-dev tk8.5-dev python-tk && \
  wget https://bootstrap.pypa.io/ez_setup.py -O - | python && \
  easy_install pip

# Define mountable directories.
VOLUME ["/data"]

# Define working directory.
WORKDIR /data

ADD requirements.txt /data/requirements.txt
RUN pip install -r /data/requirements.txt

# Define default command.
# CMD ["python"]
