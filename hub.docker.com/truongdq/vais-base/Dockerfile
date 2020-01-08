FROM phusion/baseimage:0.9.18

MAINTAINER Truong Do <truongdq54@gmail.com>

# Disable ssh.. we have docker exec
RUN rm -rf /etc/service/sshd /etc/my_init.d/00_regen_ssh_host_keys.sh
# Use baseimage-docker's init system.
#RUN echo "deb http://security.ubuntu.com/ubuntu trusty-security main" >> /etc/apt/sources.list
ADD sources.list /etc/apt/sources.list

RUN apt-get update
RUN apt-get install -y libopenblas-dev python-pip \
                       python-dev cython python-yaml vim libboost-all-dev libxml2-dev libxslt-dev swig \
                       libblas-dev git gfortran nginx-full unzip wget tmpreaper
RUN apt-get install -y g++-multilib libncurses5 libncurses5-dev

RUN pip install ws4py==0.3.2 tornado supervisor lxml superlance chainer uwsgi unidecode
RUN pip install etra requests setuptools nose coverage mock six tornado-cors statsd superslacker shortuuid
RUN pip install git+https://github.com/truongdo/ipgetter.git
# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
CMD ["/sbin/my_init"]
