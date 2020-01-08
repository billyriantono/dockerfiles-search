FROM phusion/baseimage:0.9.18
MAINTAINER Ops <thanhnam.it@gmail.com>

RUN rm -rf /etc/service/sshd /etc/my_init.d/00_regen_ssh_host_keys.sh
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y -q unzip git

RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# install ansible and support tools
RUN echo "===> Installing python, sudo, and supporting tools..."  && \
    apt-get update -y  &&  apt-get install --fix-missing          && \
    DEBIAN_FRONTEND=noninteractive         \
    apt-get install -y                     \
        python python-yaml sudo git        \
        curl gcc python-pip python-dev libffi-dev libssl-dev libmysqlclient-dev mysql-client && \
    apt-get -y --purge remove python-cffi          && \
    pip install --upgrade cffi                     && \
    \
    \
    echo "===> Installing Ansible..."   && \
    pip install ansible                 && \
    pip install --upgrade paramiko                 && \
    pip install --upgrade setuptools                 && \
    pip install MySQL-python    && \
    # \
    # \
    # echo "===> Removing unused APT resources..."                  && \
    # apt-get -f -y --auto-remove remove \
    #              gcc python-pip python-dev libffi-dev libssl-dev  && \
    apt-get clean                                                 && \
    rm -rf /var/lib/apt/lists/*  /tmp/*

CMD ["/sbin/my_init"]
