FROM python:3.6.6
MAINTAINER wuyue92tree@163.com

WORKDIR /data/src

COPY requirements.txt requirements.txt

RUN pip install -r requirements.txt -i http://mirrors.aliyun.com/pypi/simple --trusted-host mirrors.aliyun.com \
    && pip install supervisor==4.1.0 \
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

COPY supervisor.conf /etc/supervisor/supervisor.conf

# 安装nginx

ADD http://nginx.org/download/nginx-1.14.2.tar.gz /data/nginx-src/

RUN tar -xvf /data/nginx-src/nginx-1.14.2.tar.gz -C /data/nginx-src/

WORKDIR /data/nginx-src/nginx-1.14.2

RUN ./configure \
    && make \
    && make install

WORKDIR /data/src

EXPOSE 9001
EXPOSE 80

CMD supervisord -nc /etc/supervisor/supervisor.conf
