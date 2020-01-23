FROM arizonatribe/centosredis
MAINTAINER David Nunez <arizonatribe@gmail.com>

ENV APP_NAME centosredissupervisor

# Install python-related tools
RUN yum install -y \
     python \
     openssh-server \
     python-pip \
     python-setuptools \
     supervisor
RUN pip install --upgrade pip
RUN pip install supervisor-stdout
RUN easy_install supervisor

RUN yum -y clean all

CMD ["/usr/bin/start"]

# Overlay, containing supervisord configs and other shell scripts
COPY docker /

