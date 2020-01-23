FROM    centos:7
MAINTAINER "kkk" <kkk@jccsoftware.com>
RUN	yum check-update; \
  	yum -y update
RUN   	yum -y groupinstall "Development Tools";
RUN   	yum -y install gettext-devel openssl-devel perl-CPAN perl-devel zlib-devel wget;
RUN	yum -y install net-tools;
