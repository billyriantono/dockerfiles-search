FROM centos:7

RUN yum install -y epel-release && yum install -y python python-devel python-pip tesseract python-pillow python-requests python-greenlet python-gevent libffi-devel openssl-devel libxml2-devel libxslt-devel python-lxml pyOpenSSL python-cssselect python-six python-kombu python-amqp python-anyjson python-pymongo pytz gcc
RUN pip install grequests pytesseract Scrapy celery[mongodb]

ENV C_FORCE_ROOT 1
