FROM centos:centos6

USER root

# base env variables
ENV PKG_CONFIG_PATH /usr/local/lib/pkgconfig:/usr/lib64/pkgconfig
ENV PATH /opt/rh/devtoolset-2/root/usr/bin/:/opt/rh/devtoolset-2/root/usr/lib/:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# add virtdb-demo user
RUN groupadd -g 10012 virtdb-demo
RUN useradd -g 10012 --uid 10012 -G wheel,adm,cdrom virtdb-demo

# set user's home
ENV HOME /home/virtdb-demo

# prepare packages and environment
RUN yum -y update
RUN yum -y install wget

# add epel and remi repos
RUN wget http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN wget http://rpms.famillecollet.com/enterprise/remi-release-6.rpm
RUN rpm -Uvh remi-release-6*.rpm epel-release-6*.rpm
RUN rm remi-release-6*.rpm epel-release-6*.rpm

# add devtools-2 for gcc-4.8
RUN wget http://people.centos.org/tru/devtools-2/devtools-2.repo -O /etc/yum.repos.d/devtools-2.repo
RUN yum -y install devtoolset-2-binutils devtoolset-2-gcc-c++ devtoolset-2-gcc

# add neccesary tools 
RUN yum -y install tar bzip2 which file boost-devel bison flex readline-static readline-devel readline expat expat-devel
RUN yum -y install curlpp curlpp-devel libcurl-devel libcurl perl-ExtUtils-MakeMaker tcl perl-Locale-Msgfmt install vim-enhanced
RUN yum -y install gettext-devel gettext-libs openssl-devel krb5-libs krb5-devel libtool unzip gettext

# add supplementary files
ADD env-devtoolset-2.sh /etc/profile.d/
ADD env-pkgconfig.sh /etc/profile.d/

# add git 1.9.4 globally
USER root
WORKDIR /root
RUN wget https://github.com/git/git/archive/v1.9.4.tar.gz
RUN tar xfz v1.9.4.tar.gz
WORKDIR /root/git-1.9.4 
RUN make
RUN make install prefix=/usr/local

# add autoconf globally
USER root
WORKDIR /root
RUN wget http://ftp.gnu.org/gnu/autoconf/autoconf-2.69.tar.gz
RUN tar xfz autoconf-2.69.tar.gz
WORKDIR /root/autoconf-2.69 
RUN ./configure --prefix=/usr/local
RUN make 
RUN make install

# add protobuf 2.6.1 local to virtdb-demo user
USER virtdb-demo
WORKDIR /home/virtdb-demo
RUN wget https://github.com/google/protobuf/releases/download/v2.6.1/protobuf-2.6.1.tar.bz2
RUN tar xfj protobuf-2.6.1.tar.bz2
WORKDIR /home/virtdb-demo/protobuf-2.6.1
RUN ./configure --disable-shared --enable-static --without-zlib --disable-dependency-tracking --with-pic --disable-option-checking --prefix=/home/virtdb-demo/protobuf-install
RUN make
RUN make install
ENV PATH /home/virtdb-demo/protobuf-install/bin:$PATH
ENV PKG_CONFIG_PATH /home/virtdb-demo/protobuf-install/lib/pkgconfig:$PKG_CONFIG_PATH

# add libsodium local to virtdb-demo user
USER virtdb-demo
WORKDIR /home/virtdb-demo
RUN wget https://github.com/jedisct1/libsodium/releases/download/1.0.3/libsodium-1.0.3.tar.gz && tar xfz libsodium-1.0.3.tar.gz && rm libsodium-1.0.3.tar.gz 
WORKDIR /home/virtdb-demo/libsodium-1.0.3
RUN ./configure --disable-shared --enable-static --with-pic --prefix=/home/virtdb-demo/libsodium-install 
RUN make
RUN make install 
ENV PKG_CONFIG_PATH /home/virtdb-demo/libsodium-install/lib/pkgconfig:$PKG_CONFIG_PATH

# add zeromq local to virtdb-dmeo user
USER virtdb-demo
WORKDIR /home/virtdb-demo
RUN wget https://github.com/zeromq/zeromq4-x/archive/v4.0.7.tar.gz
RUN tar xfz v4.0.7.tar.gz
RUN rm v4.0.7.tar.gz 
WORKDIR /home/virtdb-demo/zeromq4-x-4.0.7
RUN ./autogen.sh 
RUN LIBS=-lstdc++ ./configure --disable-dependency-tracking --disable-shared --enable-static --with-pic --disable-libtool-lock --with-libsodium=/home/virtdb-demo/libsodium-install --prefix=/home/virtdb-demo/libzmq-install 
# --with-libsodium-include-dir
# --with-libsodium-lib-dir
RUN make 
RUN make install
ENV PKG_CONFIG_PATH /home/virtdb-demo/libzmq-install/lib/pkgconfig:$PKG_CONFIG_PATH

# add postgres 9.3 local to virtdb-demo user
USER virtdb-demo
WORKDIR /home/virtdb-demo
RUN git clone -b REL9_3_STABLE https://github.com/postgres/postgres.git
WORKDIR /home/virtdb-demo/postgres
RUN git checkout REL9_3_STABLE
RUN ./configure --prefix=/home/virtdb-demo/postgres-install --with-openssl
RUN make
RUN make install
ENV POSTGRES_VERSION 9.3
ENV PATH $PATH:/home/virtdb-demo/postgres-install/bin

# add .gpyi
USER virtdb-demo
RUN mkdir /home/virtdb-demo/.gyp
ADD include.gypi /home/virtdb-demo/.gyp/include.gypi

# install node
ENV NODE_VERSION v4.2.2
USER virtdb-demo
WORKDIR /home/virtdb-demo
RUN wget https://nodejs.org/dist/$NODE_VERSION/node-$NODE_VERSION.tar.gz
RUN tar xfz node-$NODE_VERSION.tar.gz
WORKDIR /home/virtdb-demo/node-$NODE_VERSION
RUN ./configure --prefix=/home/virtdb-demo/node-install
RUN make
RUN make install
ENV PATH /home/virtdb-demo/node-install/bin:$PATH

#instal jsawk
USER root
RUN yum -y install js-devel
USER virtdb-demo
WORKDIR /home/virtdb-demo
RUN mkdir -p jsawk-install
RUN curl -L http://github.com/micha/jsawk/raw/master/jsawk > jsawk-install/jsawk
RUN chmod u+x jsawk-install/jsawk
ENV PATH $PATH:/home/virtdb-demo/jsawk-install

USER virtdb-demo
ADD scripts /home/virtdb-demo/scripts

USER virtdb-demo
WORKDIR ${HOME}

