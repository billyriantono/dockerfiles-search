FROM ubuntu:14.04 
MAINTAINER wujin <wujin@bytedance.com>
ENV DEBIAN_FRONTEND noninteractive
RUN sed -i 's/http:\/\/archive\.ubuntu\.com\/ubuntu\//http:\/\/mirrors\.163\.com\/ubuntu\//g' /etc/apt/sources.list
RUN apt-get update && apt-get install -y \
    python-pip python-dev uwsgi-plugin-python supervisor
COPY requirements.txt /usr/share/
RUN pip install -r /usr/share/requirements.txt
