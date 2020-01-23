# base image
FROM python:3.6.5-alpine

RUN apk update && apk add netcat-openbsd postgresql-dev gcc python3-dev musl-dev

# set working directory
WORKDIR	/srv

# add and install requirements
COPY requirements.txt /srv/requirements.txt
RUN pip	install -r requirements.txt --proxy=${HTTP_PROXY}

# add code to project
COPY . /srv
