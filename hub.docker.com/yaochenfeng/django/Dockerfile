FROM python:3


RUN apt-get update && \
    apt-get install -y \
    nginx \
    supervisor \
	sqlite3 && \
	pip3 install -U pip setuptools && \
    rm -rf /var/lib/apt/lists/* && \
    pip3 install uwsgi


COPY requirements.txt docker/docker-entrypoint.sh docker/uwsgi.ini /app/
COPY docker/uwsgi.ini /app/deploy/uwsgi.ini
COPY docker/nginx-app.conf /etc/nginx/sites-enabled/default
COPY docker/supervisora-app.conf /etc/supervisor/conf.d/

ENV PYTHONUNBUFFERED 1
ENV TZ=Asia/Shanghai \
    DJANGO_PRJ="website" \
    RUN_INIT=1 \
    APP_ENV_DOCKER=1 \
    App_HEALTH_URL="http://localhost:8080/"

WORKDIR /app/code/
COPY . .
#RUN echo http://mirrors.aliyun.com/alpine/v3.6/main > /etc/apk/repositories; \
#    apk --update add --no-cache tzdata openssl-dev libffi-dev \
#    python-dev \
#    zlib-dev \
#    musl-dev \
#    libc-dev \
#    gcc \
#    mysql-client \
#    && pip install --upgrade pip

RUN chmod 755 /app/docker-entrypoint.sh && \
    mkdir /var/log/uwsgi  && \
    pip install --no-cache-dir -r requirements.txt -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com


EXPOSE 80
ENTRYPOINT ["/app/docker-entrypoint.sh"]

HEALTHCHECK CMD curl -v --fail ${App_HEALTH_URL} || exit 1