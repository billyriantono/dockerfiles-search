FROM zhaowh/centos                                                                                               
MAINTAINER  Zhao Weihong                                                                                                   

# Install gcc 
RUN yum update -y && \
    yum install -y --enablerepo=epel  \
      gcc \
      jemalloc.x86_64 \
      jemalloc-devel.x86_64  &&\
    yum clean all
                                                                                                                      
# Install Redis.
RUN \
  cd /tmp && \
  wget http://download.redis.io/redis-stable.tar.gz && \
  tar xvzf redis-stable.tar.gz && \
  cd redis-stable && \
  make && \
  make install && \
  cp -f src/redis-sentinel /usr/local/bin && \
  mkdir -p /etc/redis && \
  cp -f *.conf /etc/redis && \
  rm -rf /tmp/redis-stable* && \
  sed -i 's/^\(bind .*\)$/# \1/' /etc/redis/redis.conf && \
  sed -i 's/^\(daemonize .*\)$/# \1/' /etc/redis/redis.conf && \
  sed -i 's/^\(dir .*\)$/# \1\ndir \/data/' /etc/redis/redis.conf && \
  sed -i 's/^\(logfile .*\)$/# \1/' /etc/redis/redis.conf                                                                                                                           
                                                                                                                           
VOLUME ["/data"]

WORKDIR /data

EXPOSE 6379

CMD ["redis-server", "/etc/redis/redis.conf"]
