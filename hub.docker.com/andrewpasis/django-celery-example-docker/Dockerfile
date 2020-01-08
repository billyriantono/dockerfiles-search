FROM python:3.7-alpine

COPY ./etc /etc/

COPY ./code /code/
WORKDIR /code/

RUN apk add --no-cache libcurl
ENV PYCURL_SSL_LIBRARY=openssl

RUN apk update \
  && apk add --virtual .build-deps build-base curl-dev gcc python3-dev musl-dev \
  && apk add postgresql-dev \
  && pip install psycopg2 \
  && pip install pycurl \
  && apk del .build-deps \
  && rm -rf /var/cache/apk/* \
  && pip install --upgrade pip \
  && pip install -r /code/requirements-prod.txt \
  && pip install awscli gunicorn

EXPOSE 8000 8001
ADD entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/bin/sh","/entrypoint.sh"]

# sudo docker exec -it "$(sudo docker ps -qf name=github_blog)" sh

# python manage.py migrate
