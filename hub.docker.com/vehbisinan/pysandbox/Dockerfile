# We are using official python image:
FROM python:2.7

# Define the version:
LABEL version=0.0.1dev

# Define the maintainer:
MAINTAINER Vehbi Sinan Tunalioglu <vst@vsthost.com>

# Configure debconf:
RUN echo "debconf debconf/frontend select Noninteractive" | debconf-set-selections

# Prepare apt-get:
RUN apt-get update -qy

# Install gunicorn:
RUN apt-get install -qy nano vim emacs unzip

# Install ipython:
RUN pip install ipython

# Start with ipython
CMD ["ipython"]
