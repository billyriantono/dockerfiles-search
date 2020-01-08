FROM centos:centos7

RUN rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7 \
 && yum install -q -y epel-release \
 && yum localinstall -q -y https://download.postgresql.org/pub/repos/yum/9.6/redhat/rhel-7-x86_64/pgdg-centos96-9.6-3.noarch.rpm \
 && yum localinstall -q -y http://repo.okay.com.mx/centos/7/x86_64/release/okay-release-1-1.noarch.rpm \
 # import GPG KEYS
 && rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-EPEL-7 \
 && rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-OKAY \
 && rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-PGDG-96 \
 && yum update -q -y \
 && yum upgrade -q -y \
 && yum install -q -y \
        git \
        gcc \
        gcc-c++ \
        make \
        bzip2 \
        libyaml-devel \
        libffi-devel \
        zlib-devel \
        openssl-devel \
        readline-devel \
        gdbm-devel \
        ncurses-devel \
        ImageMagick \
        ImageMagick-devel \
        # For pry
        which \
        less \
        # For phantomjs
        fontconfig \
        # postgresql 9.6
        postgresql96-devel \
  && yum install -q -y nodejs npm --enablerepo=epel --disablerepo=okay \
  && yum install -q -y phantomjs \
  && yum clean all \
  && rm -rf /var/cache/yum

RUN curl -sO http://ftp.ruby-lang.org/pub/ruby/2.2/ruby-2.2.5.tar.gz \
 && tar -zxf ruby-2.2.5.tar.gz \
 && cd ruby-2.2.5 \
 && ./configure --disable-install-doc --without-tcl --without-tk >> /tmp/configure.out 2>&1 \
 && make -j$(getconf _NPROCESSORS_ONLN) >> /tmp/make.out 2>&1 \
 && make install >> /tmp/make.out 2>&1 || echo 'please tell me /tmp/configure.out and /tmp/make.out if build error.' \
 && cd .. \
 && rm -r ruby-2.2.5 ruby-2.2.5.tar.gz \
 && echo 'gem: --no-document' >> /usr/local/etc/gemrc \
 && gem update --system 2.7.8 \
 && gem install bundler --force -v "~>1.0"

CMD ["irb"]
