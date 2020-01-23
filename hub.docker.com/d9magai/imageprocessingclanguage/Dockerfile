FROM d9magai/imagemagick
MAINTAINER d9magai

RUN yum update -y && yum install -y epel-release && yum clean all
RUN yum install -y \
    httpd-devel \
    CUnit-devel \
    json-c-devel \
    libcurl-devel \
    openssl-devel \
    glib2-devel \
    gdb \
&&  yum clean all

