FROM centos:7.4.1708
LABEL mantainer="michele.sacchetti@aroundthecode.org"

RUN yum groupinstall -y 'Development Tools' && \
yum install -y  gem ruby-devel libffi-devel make && \
gem install travis

CMD ["/bin/bash"]
