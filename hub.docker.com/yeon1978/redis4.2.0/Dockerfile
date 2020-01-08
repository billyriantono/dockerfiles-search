FROM ubuntu:16.04

# 기본 Package 설치
RUN apt-get update \
    && apt-get install -y software-properties-common vim cron curl wget net-tools telnetd iputils-ping net-tools unzip telnet

# PHP Repository 추가
RUN LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php

# php Package 설치
RUN apt-get update \
    && apt-get install -y php7.2 && apt-get install -y php7.2-dev \
    && apt-get install build-essential -y \
    && apt-get install tcl8.5 -y

# redis-Server 다운로드 및 설치
RUN set -ex; \
    wget "http://download.redis.io/releases/redis-stable.tar.gz"; \
    tar xzf redis-stable.tar.gz; \
    mv redis-stable redis; \
    rm redis-stable.tar.gz; \
    cd redis; \
    \
    make; \
    #taskset -c 1 make test; \
    \
    make install; \
    \
    cd utils; \
    ./install_server.sh;
    #echo "/usr/local/bin/redis-server -v";

# phpredis 설치
RUN set -eux; \
    wget "https://github.com/phpredis/phpredis/archive/develop.zip"; \
    unzip develop.zip -d ./phpredis; \
    rm develop.zip; \
    mv phpredis/ /etc/ && cd /etc/phpredis; 

# build module
RUN set -eux; \
    cd /etc/phpredis/phpredis-develop; \
    phpize && ./configure && make && make install;

# redis config ini
RUN set -eux; \
    touch /etc/php/7.2/mods-available/redis.ini; \
    echo 'extension=redis.so' > /etc/php/7.2/mods-available/redis.ini; \
    echo 'extension=redis.so' >> /etc/php/7.2/cli/php.ini; \
    \
    # 모든 외부 IP 접속 허용
    sed -i 's/bind 127.0.0.1/bind 0.0.0.0/g' /redis/redis.conf; \
    # redis 보호 모드 disable
    sed -i 's/protected-mode yes/protected-mode no/g' /redis/redis.conf; \
    \
    phpenmod redis; \
    service apache2 restart;

#Expose ports
EXPOSE 6379


# protected mode no : redis에 remote 접속 가능 option 
# 1. redis-cli 에서 CONFIG SET protected-mode no 설정
# 2. /redis/redis.conf에서 protected-mode yes를 no로 변경
# 3. redis-server 시작시 --protected mode no 옵션 추가
# redis Start
CMD ["redis-server", "/redis/redis.conf"]