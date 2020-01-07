FROM centos:7

RUN yum update \
    && yum -y install wget gcc make zlib-devel openssl-devel \
    && wget https://cache.ruby-lang.org/pub/ruby/2.4/ruby-2.4.1.tar.gz \
    && tar -xf ruby-2.4.1.tar.gz \
    && cd /ruby-2.4.1 \
    && ./configure --prefix=/usr/local --disable-install-rdoc \
    && make -j $(nproc) install \
    && cd / \
    && rm -rf /ruby-2.4.1 \
    && rm ruby-2.4.1.tar.gz \
    && wget https://rubygems.org/rubygems/rubygems-2.6.12.tgz \
    && tar xf rubygems-2.6.12.tgz \
    && cp  -a /rubygems-2.6.12/bin/* /usr/local/bin/ \
    && rm rubygems-2.6.12* -rf \
    && wget -O redis.tar.gz http://download.redis.io/releases/redis-4.0.1.tar.gz \
    && tar -xzf redis.tar.gz \
    && rm -f redis.tar.gz \
    && make -C /redis-4.0.1 -j "$(nproc)" \
    && make -C /redis-4.0.1 install \
    && cp /redis-4.0.1/src/redis-trib.rb /usr/local/bin/ \
    && rm -rf /redis-4.0.1/redis \
    && gem install redis \
    && yum remove -y wget wget gcc make zlib-devel openssl-devel \
    && yum clean all \
    && mkdir /data

VOLUME /data
WORKDIR /data
EXPOSE 6379
COPY docker-entrypoint.sh /usr/local/bin/
ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["redis-server"]
