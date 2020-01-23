FROM fedora:24
RUN yum install -y systemd \
  && yum groupinstall -y "Development Tools" \
  && yum install -y python-devel zlib-devel libcurl-devel openssl-devel \
          cyrus-sasl-devel cyrus-sasl-md5 apr-devel subversion-devel apr-util-devel ruby-devel ruby
RUN gem install fpm
