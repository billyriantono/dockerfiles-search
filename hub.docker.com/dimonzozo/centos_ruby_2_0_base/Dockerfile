FROM centos
MAINTAINER dimonzozo@gmail.com

# Install dependencies.
RUN yum update -y
RUN yum install -y curl git pkgconfig wget
RUN yum install -y gcc gcc-c++ make libxml2 libxml2-devel libxslt libxslt-devel openssl-devel zlib-devel libcurl curl-devel mysql-devel mysql

RUN wget http://dl.fedoraproject.org/pub/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN rpm -ivh epel-release-6-8.noarch.rpm
RUN yum --enablerepo=epel -y install libyaml

ADD ruby-2.0.0p353-2.el6.x86_64.rpm /opt/

RUN rpm -Uvh /opt/ruby-2.0.0p353-2.el6.x86_64.rpm

# Install multiple versions of ruby
ENV CONFIGURE_OPTS --disable-install-doc

# Install Bundler for each version of ruby
RUN bash -l -c 'gem install bundler foreman --no-ri --no-rdoc'