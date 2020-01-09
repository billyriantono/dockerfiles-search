FROM python:3.7.3-alpine3.9

RUN pip install --no-cache-dir --upgrade setuptools flexget==2.21.32

VOLUME ["/root/.flexget"]

EXPOSE 5050

CMD ["flexget", "daemon", "start", "--autoreload-config"]
