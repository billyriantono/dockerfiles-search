FROM robo2025/python:3.6-alpine
ENV PYTHONUNBUFFERED 1


ADD . /project/roboserver

WORKDIR /project/roboserver

RUN apk add -U tzdata && \
   ln -sf /usr/share/zoneinfo/Asia/Shanghai  /etc/localtime

RUN pip install -r requirements.txt

CMD ["uwsgi", "/project/roboserver/glc_inventory_api/wsgi/uwsgi.ini"]
