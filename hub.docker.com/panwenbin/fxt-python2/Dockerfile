FROM python:2

RUN pip install pymysql enum34 bs4 pymongo mysql-python oss2 redis DBUtils elasticsearch flask objgraph lxml cssselect cos-python-sdk-v5 schedule \
  && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

WORKDIR /app
