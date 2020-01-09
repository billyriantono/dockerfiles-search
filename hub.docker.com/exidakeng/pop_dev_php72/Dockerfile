# 该镜像配置文档 https://dockerfile.readthedocs.io/en/latest/content/DockerImages/dockerfiles/php-nginx.html
FROM webdevops/php-nginx:7.2

# 设置时区
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update && apt-get install -y \
    openssl \
    libssl-dev \
    libcurl4-gnutls-dev \
    libmagick++-dev

# 拷贝扩展包
COPY ./pkg/imagick-3.4.3.tgz /home/imagick.tgz
COPY ./pkg/yar-2.0.4.tgz /home/yar.tgz

# 安装扩展
RUN pecl install /home/imagick.tgz \
    && pecl install /home/yar.tgz \
    # 清理扩展包源文件
    && rm -f /home/imagick.tgz \
    && rm -f /home/yar.tgz
