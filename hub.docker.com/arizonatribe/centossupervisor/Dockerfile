FROM arizonatribe/centos
MAINTAINER David Nunez <arizonatribe@gmail.com>

# Install python-related tools
RUN yum install -y \
     openssh-server \
     python \
     python-pip \
     python-setuptools \
     supervisor
RUN yum -y clean all

RUN pip install --upgrade pip
RUN pip install supervisor-stdout
RUN easy_install supervisor

