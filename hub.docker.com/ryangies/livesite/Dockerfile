FROM centos:centos7
MAINTAINER Ryan Gies <ryangies@cpan.org>

RUN yum -y update; yum clean all
RUN yum -y install epel-release deltarpm; yum clean all
RUN yum -y install \
  openssh-clients \
  which \
  gcc \
  make \
  wget \
  tar \
  rsync \
  vim \
  perl \
  perl-devel \
  perl-CPAN \
  perl-App-cpanminus \
  httpd \
  httpd-devel \
  pcre-devel \
  mod_perl \
  mod_perl-devel \
  libapreq2 \
  perl-libapreq2 \
  subversion \
  mariadb-server \
  mariadb \
  mariadb-devel \
  gd \
  gd-devel \
  anacron \
  nodejs

RUN cpanm \
  Authen::SASL \
  CGI::Cookie \
  CSS::Minifier::XS \
  Crypt::RSA \
  Data::UUID \
  DateTime \
  DateTime::TimeZone \
  Email::MIME::Creator \
  Email::Sender \
  Email::Sender::Simple \
  Email::Sender::Transport::SMTP \
  Email::Sender::Transport::SMTP::TLS \
  Email::Simple::Creator \
  Email::Valid \
  Error \
  Error::Simple \
  File::Type \
  GD \
  GD::Image \
  IO::Socket::SSL \
  Image::ExifTool \
  Image::Size \
  JSON::XS \
  JavaScript::Minifier::XS \
  LWP::Protocol::https \
  Mail::Sender \
  Math::Symbolic \
  Moose \
  Net::CIDR \
  Net::FTP::File \
  Net::Server \
  Term::Size \
  Time::CTime \
  Time::Piece \
  Try::Tiny \
  URL::Encode \
  YAML::XS

# Create runtime directories
RUN mkdir \
  /var/www/config \
  /var/www/lib \
  /var/www/logs \
  /var/www/tmp
RUN chown -R apache:apache \
  /var/www/config \
  /var/www/lib \
  /var/www/logs \
  /var/www/tmp

# Add the web server startup and configuration
COPY run-httpd.sh /run-httpd.sh
RUN chmod 755 /run-httpd.sh
COPY www-livesite.conf /etc/httpd/conf.d/www.conf

# Install the latest livesite distribution to the system
COPY install/livesite.run /tmp/livesite.run
RUN cd /tmp \
  && ./livesite.run install -y

# Install the latest lsn-execd distribution to the system
COPY install/lsn-execd.run /tmp/lsn-execd.run
RUN cd /tmp \
  && ./lsn-execd.run install -y

# Stub things out for vanilla run
COPY default/livesite.hf /var/www/config
COPY default/users /var/www/config
COPY default/index.html /var/www/html

# Default run configuration
EXPOSE 80
CMD ["/run-httpd.sh"]
