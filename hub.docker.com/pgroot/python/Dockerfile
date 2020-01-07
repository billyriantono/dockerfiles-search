FROM python:3.7
RUN pip install gunicorn && pip install celery && pip install flower
RUN apt-get update && apt-get install -y supervisor
