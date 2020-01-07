FROM python:3.6.8-slim-jessie

WORKDIR /celery
COPY ./logistics/requirements.txt /celery
COPY ./logistics/worker.py /celery
COPY ./logistics/tasks.py /celery
RUN pip install -r requirements.txt
CMD watchmedo auto-restart -d . -R -p '*.py' -- celery worker -A worker -P gevent -c 10 -l info