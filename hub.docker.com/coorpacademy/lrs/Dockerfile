FROM python:2.7.11 as web

RUN apt-get update; apt-get install -y git nginx-full

RUN pip install --upgrade pip; pip install 'fabric<2.0'

RUN mkdir /workspace; cd /workspace; git clone https://github.com/evermax/ADL_LRS.git

COPY settings.py /workspace/ADL_LRS/adl_lrs/settings.py
COPY celery.py /workspace/ADL_LRS/lrs/celery.py

RUN /bin/bash -c "cd /workspace/ADL_LRS; fab setup_env"

COPY wait-for-postgres.sh /workspace/wait-for-postgres.sh
COPY start.sh /workspace/start.sh
COPY nginx.conf /etc/nginx/sites-enabled/default

RUN mkdir -p /etc/uwsgi/vassals; mkdir /workspace/ADL_LRS/logs
COPY lrs_uwsgi.ini /etc/uwsgi/vassals/lrs_uwsgi.ini

EXPOSE 8080
CMD ["/workspace/start.sh"]


FROM web as worker

COPY worker.sh /workspace/worker.sh

CMD ["/workspace/worker.sh"]