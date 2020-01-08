
#
# https://github.com/IBBD/ubuntu
#
# sudo docker build -t ibbd/ubuntu ./
#

# Pull base image.
FROM ubuntu

MAINTAINER reflying "278432993@qq.com"

RUN \
	apt update               \
	&& apt install -y libffi-dev libssl-dev python-dev  libxml2-dev libxslt1-dev \
	&& apt install python -y  \
	&& apt install ipython -y  \
	&& apt install python-pip -y    \
	&& pip install scrapy          \
    && pip install redis \
    && pip install PyMySQL \
    && pip install scrapy-redis



# 解决时区问题
ENV TZ "Asia/Shanghai"

# 终端设置
# 默认值是dumb，这时在终端操作时可能会出现：terminal is not fully functional
ENV TERM xterm

# Define mountable directories.
VOLUME /var/www

# 工作目录
WORKDIR /var/www/crawler 