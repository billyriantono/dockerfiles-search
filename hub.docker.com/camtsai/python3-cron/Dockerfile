FROM registry.docker-cn.com/library/python:3.6

RUN apt-get update
RUN apt-get install -y cron
RUN echo 'Asia/Shanghai' >/etc/timezone & cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

WORKDIR /project

ENV LC_ALL="C.UTF-8" LANG="C.UTF-8" PYTHONPATH=/project:$PYTHONPATH
COPY default_env.sh /etc/profile.d/

