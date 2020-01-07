FROM centos
# packages
RUN yum groupinstall -y "Development tools"
RUN yum -y install openssl openssl-devel readline-devel readline compat-readline5 libxml2-devel libxslt-devel libyaml-devel git
# rbenv
RUN git clone https://github.com/sstephenson/rbenv.git ~/.rbenv
RUN mkdir -p ~/.rbenv/plugins && git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
RUN echo -e 'export PATH=~/.rbenv/bin:$PATH\neval "$(rbenv init -)"' >> /etc/profile.d/rbenv.sh && source /etc/profile.d/rbenv.sh
# ruby
ENV CONFIGURE_OPTS --disable-install-doc
RUN bash -lc '~/.rbenv/plugins/ruby-build/bin/ruby-build 1.9.3-p545 ~/.rbenv/versions/1.9.3'
RUN bash -lc '~/.rbenv/plugins/ruby-build/bin/ruby-build 2.0.0-p451 ~/.rbenv/versions/2.0.0'
RUN bash -lc '~/.rbenv/plugins/ruby-build/bin/ruby-build 2.1.1 ~/.rbenv/versions/2.1'
# bundler for all ruby
RUN echo 'gem: --no-rdoc --no-ri' >> /.gemrc
RUN bash -lc 'for v in 1.9.3 2.0.0 2.1; do rbenv global $v; gem install bundler; done'
# mongodb (2.4.9)
RUN rpm -ivh http://downloads-distro.mongodb.org/repo/redhat/os/x86_64/RPMS/mongo-10gen-2.4.9-mongodb_1.x86_64.rpm http://downloads-distro.mongodb.org/repo/redhat/os/x86_64/RPMS/mongo-10gen-server-2.4.9-mongodb_1.x86_64.rpm
RUN echo 'smallfiles = true' >> /etc/mongod.conf # make journal small
RUN /etc/init.d/mongod start && /etc/init.d/mongod stop
# memcached (1.4.4-3.el6)
RUN echo "NETWORKING=yes" >/etc/sysconfig/network
RUN yum -y install memcached
RUN /etc/init.d/memcached start && /etc/init.d/memcached stop
# mysql (5.5.36-1)
RUN rpm -ivh  http://ftp-srv2.kddilabs.jp/Linux/distributions/fedora/epel/6/x86_64/epel-release-6-8.noarch.rpm
RUN rpm -ivh http://rpms.famillecollet.com/enterprise/remi-release-6.rpm
RUN yum -y install mysql-server --enablerepo=remi
RUN /etc/init.d/mysqld start && /etc/init.d/mysqld stop
# redis (2.8.6)
RUN wget http://download.redis.io/releases/redis-2.8.6.tar.gz && tar xzf redis-2.8.6.tar.gz && cd redis-2.8.6 && make && make install
RUN sed 's/daemonize no/daemonize yes/' redis-2.8.6/redis.conf > /etc/redis.conf
#RUN /usr/local/bin/redis-server /etc/redis.conf