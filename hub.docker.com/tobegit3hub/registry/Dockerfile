
FROM ubuntu:14.10
MAINTAINER tobe <tobeg3oogle@gmail.com>

# Update
RUN apt-get update

# Install pip
RUN apt-get -y install python-pip

# Install dependencies for backports.lzma (python2 requires it)
RUN apt-get -y install python-dev liblzma-dev libevent1-dev

# Install docker-registry
RUN pip install flask-cors docker-registry docker-registry-driver-fdsstorage

ADD . /docker-registry-driver-fdsstorage

ENV DOCKER_REGISTRY_CONFIG /docker-registry-driver-fdsstorage/config/config_fdsstorage.yml
ENV SETTINGS_FLAVOR fdsstorage

# ENV FDS_DOMAIN=FDS_DOMAIN
# ENV FDS_BUCKET=YOUR_BUCKET
# ENV QINIU_ACCESSKEY=YOUR_ACCESSKEY
# ENV QINIU_SECRETKEY=YOUR_SECRETKEY

EXPOSE 5000

CMD ["docker-registry"]

