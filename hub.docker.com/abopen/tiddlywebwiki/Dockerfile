FROM python:2-alpine
MAINTAINER Andrew Back <andrew@abopen.com>

VOLUME /data

RUN mkdir /usr/src/tww

COPY . /usr/src/tww
WORKDIR /usr/src/tww

RUN pip install -r requirements.txt

ENTRYPOINT ["/usr/src/tww/entrypoint.sh"]

EXPOSE 80
