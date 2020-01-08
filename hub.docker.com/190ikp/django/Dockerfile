FROM python:3.6.8-slim-stretch

ENV DJANGO_VER="2.2"

WORKDIR /usr/src/app
COPY . .
RUN pip install --no-cache-dir Django==${DJANGO_VER}

EXPOSE 8000