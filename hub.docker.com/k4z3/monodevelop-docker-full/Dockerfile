FROM k4z3/monodevelop
MAINTAINER karl.zerlauth@gmail.com
ENV REFRESHED_AT 2017-04-27

RUN apt-get update && apt-get install -y curl autoconf automake tcl libtool make g++ unzip liblmdb-dev libhiredis-dev libgrpc-dev unzip && \
curl -OL https://github.com/google/protobuf/releases/download/v3.2.0/protoc-3.2.0-linux-x86_64.zip && \
unzip protoc-3.2.0-linux-x86_64.zip -d protoc3 && \
mv protoc3/bin/protoc /usr/bin/protoc && \
cd /tmp && \
curl -O http://download.redis.io/redis-stable.tar.gz && tar xzvf redis-stable.tar.gz && \
cd redis-stable && make && make install && mkdir /etc/redis && cp /tmp/redis-stable/redis.conf /etc/redis && rm -rf /tmp && rm -rf /var/lib/apt/lists/* 


WORKDIR /home


CMD [ "/usr/local/bin/monodevelop" ]

