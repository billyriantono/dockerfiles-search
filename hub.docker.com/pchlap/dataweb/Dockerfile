FROM ubuntu:18.04

EXPOSE 8000

ENV PYTHONUNBUFFERED 1

# Make a directory used for extracting archives files
RUN mkdir -p /work && \
    mkdir /data && mkdir /data/db && \
    chmod a+w /data/db

# Copy requirements.txt to working directory
ADD requirements.txt /projects/
ADD requirements-dev.txt /projects/

# Install libraries required by python-ldap as well as Redis server for celery and memcached for django-cache
RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get -y install libsasl2-dev \
    libldap2-dev \
    libssl-dev \
    freetds-dev \
    libmysqlclient-dev \
    python3-pip \
    memcached \
    git 
    
    #ln -fs /usr/share/zoneinfo/Australia/Sydney /etc/localtime && \
    #dpkg-reconfigure --frontend noninteractive tzdata

RUN ln -s /usr/bin/python3 /usr/bin/python
RUN ln -s /usr/bin/pip3 /usr/bin/pip

# Install Python packages defined in requirements.txt
RUN pip install -r /projects/requirements.txt
RUN pip install -r /projects/requirements-dev.txt

# Start Redis server for celery and memcached for Django cache
ENTRYPOINT memcached -u root
