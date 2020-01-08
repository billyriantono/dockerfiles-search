FROM python:3.6-slim

ENV PYTHONUNBUFFERED 1

# RUN apt install --no-cache shadow
RUN useradd --user-group --create-home --home-dir /flask --shell /bin/false flask

RUN apt-get update && apt-get install -y \
    gcc  
# libxml2-dev libxslt-dev libffi-dev 
# postgresql-dev

WORKDIR /flask/src

COPY ./requirements-dev.txt requirements-dev.txt
RUN pip install --no-cache-dir -r requirements-dev.txt

COPY ./requirements.txt requirements.txt
RUN pip install --no-cache-dir -r requirements.txt
