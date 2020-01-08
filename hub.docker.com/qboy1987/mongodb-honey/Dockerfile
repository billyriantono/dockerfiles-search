FROM python:3.7.4-alpine3.10
MAINTAINER "LalonSec <qiuguowei@jingweixinan.com>"

RUN mkdir /mongoproxy

COPY requirements.txt /mongoproxy/requirements.txt
ENV PYTHONPATH=/mongoproxy

RUN cd /mongoproxy && \
    apk update && \
    apk add --no-cache tzdata gcc make python3-dev musl-dev && \
 # GM+8
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    date && \
    pip3 install --no-cache-dir -r requirements.txt -i https://mirrors.aliyun.com/pypi/simple/ && \

	apk del --purge tzdata gcc make  python3-dev musl-dev


COPY LICENSE /mongoproxy
COPY README.md /mongoproxy
COPY libs /mongoproxy/libs
COPY runner.py /mongoproxy
COPY startup.sh /mongoproxy

EXPOSE 27017/tcp

WORKDIR /mongoproxy

#CMD python3 runner.py --config /mongoproxy/proxy.cfg
#CMD /bin/bash
CMD python3 runner.py -c /mongoproxy/proxy.cfg