FROM redis:5.0
MAINTAINER bonza "bonzaphp@gmail.com"

# set timezome
ENV TZ=Asia/Shanghai

RUN  mv /etc/apt/sources.list /etc/apt/sources.list.bak

COPY $PWD/sources.list /etc/apt/
# 如果网络下载比较慢的话，可以直接复制到镜像
COPY $PWD/gosu /usr/local/bin/
COPY $PWD/redis.conf /usr/local/etc/redis/redis.conf

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
    &&  apt-get update \
    &&  apt-get install -y --no-install-recommends wget \
   #&&  wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/1.11/gosu-amd64" \
   #&&  groupadd -r -g redis \
   #&&  useradd -r -g redis redis 
    &&  echo "Clean cache ================> " \
    &&  apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
    &&  apt-get clean \
    &&  chmod +x /usr/local/bin/gosu \
    &&  gosu nobody true
USER redis
# CMD ["exec", "gosu","redis","redis-server","/usr/local/etc/redis/redis.conf"]
CMD ["redis-server","/usr/local/etc/redis/redis.conf"]