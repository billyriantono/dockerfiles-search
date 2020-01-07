# Use an official Python runtime as a parent image
FROM python:3.6.8-slim-jessie

WORKDIR /logistics
COPY ./logistics/requirements.txt /logistics
COPY ./logistics/server.py /logistics
COPY ./logistics/tasks.py /logistics
COPY ./logistics/worker.py /logistics
RUN pip install -r requirements.txt

CMD gunicorn --workers=1 --reload --reload-engine=poll --worker-class=gevent -b 0.0.0.0:8000 server:app