FROM jupyter/datascience-notebook
MAINTAINER Dengcheng Yan "yandengcheng@gmail.com"

RUN pip install sqlalchemy pymysql

ADD graph-tool.list /etc/apt/sources.list.d/graph-tool.list
RUN apt-get update && apt-get install -y --force-yes python-graph-tool python3-graph-tool