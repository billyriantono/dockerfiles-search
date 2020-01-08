FROM python:3.6-alpine

# Install required packages
RUN apk add --no-cache --virtual .build-deps gcc linux-headers musl-dev

COPY ./requirements.txt /tmp/requirements.txt
RUN pip install -r /tmp/requirements.txt

# PYTHONUNBUFFERED 1 - Force the stdout and stderr streams to be unbuffered.
ENV PYTHONUNBUFFERED 1

# Default django settings
ENV DJANGO_SETTINGS_MODULE=mysite.settings

RUN mkdir /mysite

COPY ./mysite /mysite

WORKDIR /mysite
CMD ["uwsgi", "--http", ":8000", "--module", "mysite.wsgi"]
