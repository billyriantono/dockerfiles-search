FROM centos:latest
RUN yum install -y git tar gcc make curl-devel expat-devel gettext-devel readline-devel openssl-devel gcc-c++ autoconf 
RUN git clone https://github.com/sstephenson/rbenv.git /root/.rbenv
RUN git clone https://github.com/sstephenson/ruby-build.git /root/.rbenv/plugins/ruby-build
RUN echo 'export PATH="/root/.rbenv/bin:$PATH"' > /etc/profile.d/rbenv-path-setup.sh
RUN echo 'eval "$(rbenv init -)"' >> /etc/profile.d/rbenv-path-setup.sh
RUN /bin/bash --login -c 'rbenv install 2.1.3'

ENV HOME /root

CMD ["/bin/bash","--login"]
