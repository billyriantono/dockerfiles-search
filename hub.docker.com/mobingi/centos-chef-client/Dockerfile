FROM centos:centos7
MAINTAINER David Siaw "david.siaw@mobingi.com"

RUN yum install -y curl make automake gcc gcc-c++ kernel-devel libxml2-dev libxslt-dev git autoconf tar

RUN curl -L https://www.opscode.com/chef/install.sh | bash 
  
RUN /opt/chef/embedded/bin/gem install berkshelf
