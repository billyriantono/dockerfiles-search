FROM python:3.7-alpine

RUN set -x && \
    apk add --update \
    python \
    python-dev \
    py-pip \
    build-base \
    postgresql-dev

RUN mkdir -p /workspace

WORKDIR /usr/src/app
COPY requirements*.txt ./
RUN pip install --upgrade pip
RUN pip install --no-cache-dir -r requirements.txt


CMD ["python"]
