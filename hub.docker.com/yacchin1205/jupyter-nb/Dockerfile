FROM ubuntu:14.04

MAINTAINER Satoshi Yazawa https://github.com/yacchin1205/

# modify locale
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && apt-get install -y language-pack-en
ENV LANGUAGE en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8

RUN locale-gen en_US.UTF-8
RUN dpkg-reconfigure locales

# install related packages
RUN apt-get update && apt-get install -y nodejs-legacy npm python-virtualenv python-dev git

# ensure setuptools/pip are up-to-date
RUN pip install --upgrade setuptools pip

# install the latest version of jupyter from GitHub
RUN git clone https://github.com/jupyter/notebook.git /usr/local/notebook
RUN cd /usr/local/notebook; pip install --pre -e .

# prepare a data directory for jupyter notebook
RUN mkdir -p /var/lib/notebook

EXPOSE 8888
CMD jupyter notebook --ip=0.0.0.0 --port=8888 --notebook-dir=/var/lib/notebook
