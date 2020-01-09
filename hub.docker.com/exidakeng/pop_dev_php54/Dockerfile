FROM webdevops/php-nginx:centos-7

# 设置时区
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN yum install -y \
    gcc \
    re2c \
    openssl openssl-devel \
    php-devel \
    curl-devel

# 拷贝扩展包
COPY ./pkg/mongo-1.6.16.tgz /home/mongo.tgz
COPY ./pkg/imagick-3.4.3.tgz /home/imagick.tgz
COPY ./pkg/yar-1.2.4.tgz /home/yar.tgz

# 安装扩展
RUN pecl install /home/mongo.tgz \
    && pecl install /home/imagick.tgz \
    && pecl install /home/yar.tgz \
    # 清理扩展包源文件
    && rm -f /home/mongo.tgz \
    && rm -f /home/imagick.tgz \
    && rm -f /home/yar.tgz