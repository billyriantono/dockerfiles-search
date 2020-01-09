FROM python:3-alpine

RUN apk add \
--no-cache \
--virtual .build-deps \
gcc \
musl-dev \
libffi-dev \
libressl-dev

COPY requirements.txt .
RUN python -m pip install -r requirements.txt

RUN apk del .build-deps


COPY ./*.py ./
ENTRYPOINT ["python", "--version"]