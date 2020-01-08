FROM python:2-alpine3.7

MAINTAINER Virink <virink@outlook.com>

COPY . /app

WORKDIR /app

RUN pip install -r requirements.txt && \
	chmod +w xssor/probe

EXPOSE 5000

ENTRYPOINT [ "/usr/local/bin/python","manage.py","runserver","--insecure","0.0.0.0:5000"]
