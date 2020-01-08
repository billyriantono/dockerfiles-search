FROM python:3.6.8-alpine
ENV PYTHONUNBUFFERED 1  

RUN apk update && \
    apk add --virtual build-deps gcc python-dev musl-dev && \
    apk add jpeg-dev zlib-dev postgresql-dev postgresql-client bash fish

RUN mkdir /config  
ADD /config/requirements.txt /config/  
RUN pip install -r /config/requirements.txt
RUN pip install https://github.com/darklow/django-suit/tarball/v2
RUN mkdir /src
WORKDIR /src

