FROM centos:centos7

RUN yum -y update
RUN yum install -y centos-release-scl && \
    INSTALL_PKGS="epel-release \
     libffi \
     libffi-devel \
     python27 python27-python-devel python27-python-setuptools python27-python-pip \
     pytz \
     make \
     gcc \
     gcc-c++ \
     tar \
     curl \
     python-lxml \
     libxslt-devel \
     unixODBC-devel \
     mariadb-devel \
     httpd httpd-devel" && \
    yum install -y --setopt=tsflags=nodocs --enablerepo=centosplus $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS && \
    # Remove centos-logos (httpd dependency, ~20MB of graphics) to keep image
    # size smaller.
    rpm -e --nodeps centos-logos && \
    yum clean all -y

#RUN easy_install -U pip
RUN yum install -y python-devel python-setuptools python-pip

RUN curl --silent --location https://rpm.nodesource.com/setup_4.x | bash -
RUN yum -y install nodejs