FROM python:3.6

MAINTAINER Ulrich Petri <docker@ulo.pe>

RUN apt update && \
	apt upgrade -y && \
	pip install --upgrade pip && \
	mkdir /app && \
	python3 -m venv /venv && \
	/venv/bin/pip install fabric3

ADD . /app

WORKDIR /app

RUN /bin/bash -c "source /venv/bin/activate && fab reqs"

EXPOSE 8000

ENTRYPOINT ["/venv/bin/python", "/app/manage.py"]
