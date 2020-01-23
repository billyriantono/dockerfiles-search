FROM python:2-alpine

RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories && apk update && apk add docker

ADD dockerpuller /dockerpuller
ADD requirements.txt /requirements.txt
WORKDIR /
RUN pip install -r requirements.txt
WORKDIR /dockerpuller

VOLUME ["/var/run/docker.sock"]

ENTRYPOINT ["python", "app.py"]

