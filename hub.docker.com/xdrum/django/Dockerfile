FROM centos:6

MAINTAINER Alessio Cassibba (x-drum) <swapon@gmail.com>

RUN yum update -y && yum upgrade -y && yum clean all

RUN yum install -y centos-release-SCL
RUN yum install -y python27
ENV PATH /opt/rh/python27/root/usr/bin:$PATH
ENV LD_LIBRARY_PATH /opt/rh/python27/root/usr/lib64:$LD_LIBRARY_PATH
ENV MANPATH /opt/rh/python27/root/usr/share/man:$MANPATH

RUN easy_install pip
RUN pip install gunicorn
ENV DJANGO_VERSION 1.6.10
RUN pip install django==${DJANGO_VERSION}

VOLUME ["/data"]
WORKDIR /data

EXPOSE 8000
CMD ["/bin/bash","-c","gunicorn -v"]
