# AWS Lambda execution environment is based on Amazon Linux 1
FROM amazonlinux:1

# Install Python 3.6
RUN yum -y install python36 python36-pip

# Install your dependencies
RUN curl -s https://bootstrap.pypa.io/get-pip.py | python3
RUN yum -y install python36-devel mysql-devel gcc findutils

# Set the same WORKDIR as default image
RUN mkdir /var/task
ADD libmysqlclient.so.1020 /var/task/libmysqlclient.so.1020
WORKDIR /var/task