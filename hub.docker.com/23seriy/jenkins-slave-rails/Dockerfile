FROM centos:centos6

MAINTAINER Sergei Olshanetski <sergei@tikalk.com>

ENV HOME /root
CMD ["/bin/bash", "-l"]

RUN yum -y install curl wget which tar vim git rubygems mysql-devel ed
RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys D39DC0E3
ADD mongodb-org-2.6.repo /etc/yum.repos.d/mongodb-org-2.6.repo
RUN yum -y install mongodb-org
RUN yum install -y libxml2-devel libxslt libxslt-devel
RUN yum install -y postgresql-devel

#install required ruby versions
RUN \curl -sSL https://get.rvm.io | bash -s stable --ruby=2.0 \ 
	&& curl -sSL https://get.rvm.io | bash -s stable --ruby=2.2.0 \
	&& curl -sSL https://get.rvm.io | bash -s stable --ruby=2.1.2 \
        && curl -sSL https://get.rvm.io | bash -s stable --ruby=2.1.0 \
        && curl -sSL https://get.rvm.io | bash -s stable --ruby=1.9.3

RUN source /usr/local/rvm/scripts/rvm
RUN gem install bundler
RUN gem sources --add https://rubygems.org/

#download and install R and its dependencies
RUN su -c 'rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm' \
	&& yum -y install R \
	&& wget http://cran.r-project.org/src/contrib/Rcpp_0.12.0.tar.gz \
	&& wget http://cran.r-project.org/src/contrib/plyr_1.8.3.tar.gz \
	&& wget http://cran.r-project.org/src/contrib/reshape_0.8.5.tar.gz \
	&& R CMD INSTALL Rcpp_0.12.0.tar.gz \
	&& R CMD INSTALL plyr_1.8.3.tar.gz \
	&& R CMD INSTALL reshape_0.8.5.tar.gz

RUN yum install -y jq
RUN yum install -y bc
RUN curl --silent --location https://rpm.nodesource.com/setup | bash -
RUN yum install -y nodejs
ENV PRIVATE_GEM_PASSWORD=i909boREG
