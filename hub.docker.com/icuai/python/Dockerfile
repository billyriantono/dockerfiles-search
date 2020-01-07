FROM python:3.6-jessie

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
ENV TZ Asia/Shanghai
ONBUILD COPY requirements.txt /usr/src/app/
ONBUILD RUN pip install -i https://pypi.tuna.tsinghua.edu.cn/simple --no-cache-dir -r requirements.txt

ONBUILD COPY . /usr/src/app

