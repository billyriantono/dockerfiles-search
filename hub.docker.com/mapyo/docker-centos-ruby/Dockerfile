FROM centos:7
MAINTAINER @mapyo

RUN yum -y update; yum clean all
RUN yum install -y git gcc  make openssl-devel readline-devel; yum clean all
RUN git clone git://github.com/tagomoris/xbuild.git /usr/local/xbuild
RUN /usr/local/xbuild/ruby-install 2.2.3 /usr/local/ruby-2.2.3; rm -rf /var/tmp/ruby-build*

ENV PATH /usr/local/ruby-2.2.3/bin:$PATH
RUN gem install bundler --no-document

CMD [ "irb" ]
