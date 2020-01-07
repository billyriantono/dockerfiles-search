#
# Golang Dockerfile
# 主要为了满足高并发接口而开发
#
# 1. 手动安装包：https://gopm.io/download
# 2. golang.org的包无法安装可以到github.com/golang上查找
#
# https://github.com/ibbd/dockerfile-go
#
# sudo docker build -t ibbd/golang ./
#

# Pull base image.
FROM golang

MAINTAINER Alex Cai "cyy0523xc@gmail.com"
   
# 安装守护进程
RUN apt-get update \
    && apt-get install -y  supervisor \
    && mkdir -p  /var/log/supervisor \
    && apt-get autoremove \
    && apt-get clean \
    && rm -r /var/lib/apt/lists/*

# Get packages
# Gopm - Go Package Manager
# Gopm [global options] command [command options] [arguments...]
    #&& go get github.com/ant0ine/go-json-rest/rest \
    #&& go get github.com/shykes/spdy-go \
    #&& go get -u github.com/kataras/iris \
    #&& go get github.com/graphql-go/graphql \
    #&& go get github.com/asaskevich/govalidator \
    #&& go get github.com/dgrijalva/jwt-go \
    #&& go get gopkg.in/hlandau/passlib.v1 \
    #&& go get golang.org/x/tools \
    #&& go get golang.org/x/crypto \
    #&& go get golang.org/x/text \
    #&& go get golang.org/x/sys \
    #&& go get -u -d -t github.com/tinylib/msgp \
RUN \
    go get golang.org/x/net/context \
    && go get github.com/joho/godotenv \
    && go get github.com/go-sql-driver/mysql \
    && go get github.com/garyburd/redigo/redis \
    && go get labix.org/v2/mgo \
    && echo "nameserver 114.114.114.114" >> /etc/resolv.conf

# 解决时区问题
ENV TZ "Asia/Shanghai"

# 终端设置
# 执行php-fpm时，默认值是dumb，这时在终端操作时可能会出现：terminal is not fully functional
ENV TERM xterm

# Define mountable directories.
VOLUME /var/www

# 工作目录
WORKDIR /var/www 

EXPOSE 8080 8081 8082
CMD ["/usr/bin/supervisord"]
