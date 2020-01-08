FROM centos
# packages
RUN yum groupinstall -y "Development tools"
RUN yum -y install openssl openssl-devel readline-devel readline compat-readline5 libxml2-devel libxslt-devel libyaml-devel git
# rbenv
RUN git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
RUN mkdir -p ~/.rbenv/plugins && git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
RUN echo -e 'PATH=~/.rbenv/bin:$PATH\neval "$(rbenv init -)"' >> /etc/profile.d/rbenv.sh
# ruby
ENV CONFIGURE_OPTS --disable-install-doc
RUN bash -lc '~/.rbenv/plugins/ruby-build/bin/ruby-build 1.9.3-p545 ~/.rbenv/versions/1.9.3'
RUN bash -lc '~/.rbenv/plugins/ruby-build/bin/ruby-build 2.0.0-p451 ~/.rbenv/versions/2.0.0'
RUN bash -lc '~/.rbenv/plugins/ruby-build/bin/ruby-build 2.1.1 ~/.rbenv/versions/2.1'
# bundler for all ruby
RUN echo 'gem: --no-rdoc --no-ri' >> /.gemrc
RUN bash -lc 'for v in 1.9.3 2.0.0 2.1; do rbenv global $v; gem install bundler; done'