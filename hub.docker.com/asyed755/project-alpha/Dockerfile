FROM python:3.4

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        postgresql-client \
&& rm -rf /var/lib/apt/lists/*

WORKDIR /app/api


COPY requirements.txt /app/api
COPY . /app/api
EXPOSE 8000


RUN pip install -r requirements.txt


CMD [ "python", "./manage.py runserver 0.0.0.0:8000" ]
