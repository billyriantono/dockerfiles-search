# "ported" from https://registry.hub.docker.com/_/buildpack-deps/

FROM centos:centos7
MAINTAINER Sherwin Daganato <sherwin@daganato.com>

RUN yum -y update && yum clean all
RUN yum -y install epel-release && yum clean all
RUN yum -y install bzr cvs git mercurial subversion && yum clean all
RUN yum -y install curl wget tar && yum clean all
RUN yum -y groupinstall 'Development Tools' && yum clean all
RUN yum -y install ImageMagick \
                   bzip2-devel \
                   libcurl-devel \
                   libevent-devel \
                   libffi-devel \
                   glib2-devel \
                   libjpeg-devel \
                   ImageMagick-devel \
                   mysql-devel \
                   ncurses-devel \
                   postgresql-devel \
                   readline-devel \
                   sqlite-devel \
                   openssl-devel \
                   libxml2-devel \
                   libxslt-devel \
                   libyaml-devel \
                   zlib-devel && yum clean all 
