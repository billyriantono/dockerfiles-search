FROM	python:3.6-alpine

RUN	mkdir -p /opt/app
COPY	requirements.txt /opt/app/requirements.txt
WORKDIR /opt/app
RUN	pip install -r requirements.txt
