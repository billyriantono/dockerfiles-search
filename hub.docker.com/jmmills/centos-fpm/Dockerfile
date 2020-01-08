FROM centos:latest
MAINTAINER = Jason M. Mills <jmmills@cpan.org>
RUN cat /etc/redhat-release
RUN yum install -y gcc gcc-c++ make autoconf autotools
RUN yum install -y ruby
RUN yum install -y ruby-devel
RUN yum install -y rubygems
RUN yum install -y rpm-build
RUN gem install fpm

CMD ["/bin/bash", "-l"]
