# Centos 6 + HTTPD install 
FROM centos:centos6
MAINTAINER José Gonçalves <jose.goncalves@dlcproduction.ch>
LABEL Vendor="CentOS+HTTPD"
LABEL License="GPLv2"

# Update and install some packages.
RUN yum install -y \
    curl \
    epel-release \
    httpd \
    vim \
    htop \
    iftop \
RUN yum update -y

# default command :
CMD ["/bin/bash"]
