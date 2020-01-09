FROM centos:8

RUN yum groupinstall -y "Development Tools" \
 && yum install -y --nogpgcheck epel-release \
 && yum install -y --nogpgcheck ruby ruby-devel ruby-libs rubygems rpm-build \
 && gem install fpm --no-rdoc --no-ri \
 && yum install -y --nogpgcheck \
  byacc \
  bzip2-devel \
  cmake \
  curl-devel \
  cyrus-sasl-devel \
  freetype-devel \
  glibc-devel \
  gmp-devel \
  httpd-devel \
  krb5-devel \
  libXpm-devel \
  libc-client-devel \
  libev-libevent-devel \
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
  perl-DBI \
  perl-ExtUtils-MakeMaker \
  postgresql-devel \
  readline-devel \
  rpm-build \
  screen \
  smtpdaemon \
  sqlite-devel \
  tk-devel \
  unixODBC-devel \
  wget \
  which \
  zlib-devel \
 && yum clean all

RUN yum install -y --nogpgcheck \
  nss-devel
# && yum install --enablerepo=PowerTools -y --nogpgcheck libnsl2-devel \

ENV BUILDROOT="/root/rpmbuild"
WORKDIR /usr/local/src

# gcc 4.4.7
COPY build/rpms rpms
RUN rpm -ivh --force rpms/*.rpm
# ENV CXXFLAGS="-std=gnu++98"
# RUN update-alternatives \
#  --install /usr/bin/gcc gcc /usr/bin/gcc44 20 \
#  --slave   /usr/bin/g++ g++ /usr/bin/g++44
# ENV CC=/usr/bin/gcc44
# ENV CXX=/usr/bin/g++44
# ENV CXXFLAGS=
