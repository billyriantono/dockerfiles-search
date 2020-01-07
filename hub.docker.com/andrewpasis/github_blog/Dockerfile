FROM python:3.7-alpine

COPY ./code /code/
WORKDIR /code/

RUN apk update \
  && apk add --virtual build-deps gcc python3-dev musl-dev \
  && apk add postgresql-dev \
  && pip install psycopg2 \
  && apk del build-deps \
  && pip install --upgrade pip \
  && pip install -r /code/requirements-prod.txt \
  && pip install awscli gunicorn

EXPOSE 8000 8001
ADD entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/bin/sh","/entrypoint.sh"]

# sudo docker exec -it "$(sudo docker ps -qf name=github_blog)" sh

# python manage.py migrate
# python manage.py runserver 0.0.0.0:8001

# python manage.py collect_github

# rm -fr /html
# python manage.py staticgen http://127.0.0.1:8000 /html
