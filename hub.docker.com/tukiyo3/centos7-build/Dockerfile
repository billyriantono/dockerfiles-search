FROM centos:7

# libmcryptがepelで配布
RUN yum install -y -q epel-release && yum clean all

# centos7にあるが centos8にないもの
RUN yum install -y \
    aspell-devel \
    db4-devel \
    enchant-devel \
    libedit-devel \
    libtidy-devel \
    recode-devel \
    t1lib \
    t1lib-devel \
 && yum clean all

# centos8にもあるもの
RUN yum install -y \
    bzip2-devel \
    curl-devel \
    cyrus-sasl-devel \
    freetype-devel \
    gcc \
    gcc-c++ \
    glibc-devel \
    gmp-devel \
    httpd-devel \
    krb5-devel \
    libXpm-devel \
    libc-client-devel \
    libicu-devel \
    libjpeg-devel \
    libmcrypt-devel \
    libmhash-devel \
    libpng-devel \
    libtool \
    libtool-ltdl-devel \
    libxml2-devel \
    libxslt-devel \
    make \
    mysql-devel \
    ncurses-devel \
    net-snmp-devel \
    openldap-devel \
    openssl-devel \
    pam-devel \
    patch \
    pcre-devel \
    postgresql-devel \
    readline-devel \
    rpm-build \
    smtpdaemon \
    sqlite-devel \
    unixODBC-devel \
    wget \
    which \
    zlib-devel \
  && yum clean all

# fpm
RUN yum -y install ruby ruby-devel ruby-libs rubygems rpm-build \
 && gem install fpm --no-rdoc --no-ri

# GCC 4.4
ENV PACKAGES="compat-gcc-44 compat-gcc-44-c++"
RUN yum install -y -q $PACKAGES && yum clean all \
 && yum remove -y gcc gcc-c++ \
 && update-alternatives \
 --install /usr/bin/gcc gcc /usr/bin/gcc44 20 \
 --slave   /usr/bin/g++ g++ /usr/bin/g++44
ENV CC=/usr/bin/gcc44
ENV CXX=/usr/bin/g++44

# mysql 4.0.30
RUN yum install -y -q \
  ORBit2-devel perl-DBD-MySQL \
 && yum clean all

# php 5.2.17
RUN yum install -y -q \
  re2c byacc \
 && yum clean all

# ruby 1.8.7
RUN yum install -y -q \
  tk-devel tclx \
 && yum clean all

ENV BUILDROOT="/root/rpmbuild"
WORKDIR /usr/local/src
