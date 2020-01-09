FROM python:3-slim

RUN pip install puaa==0.3.2
COPY uaa.yml /etc/uaa.yml

EXPOSE 8000
ENV AUTHLIB_INSECURE_TRANSPORT=true
CMD gunicorn -k gevent -b 0.0.0.0 puaa.app:app
