FROM python:3.7-alpine
COPY requirements.txt .
RUN apk add --no-cache \
    build-base \
    openssl-dev \
    libffi-dev \
  && pip install -r requirements.txt \
  && apk del build-base \
  && rm -rf /var/cache/apk/*
COPY fastdns-to-terraform.py .
CMD python fastdns-to-terraform.py

