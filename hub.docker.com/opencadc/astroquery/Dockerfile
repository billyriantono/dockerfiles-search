FROM python:3.7-alpine

WORKDIR /usr/src/app
ENV ENV="PROD"

COPY requirements.txt ./
COPY entrypoint.sh /entrypoint.sh

RUN apk --no-cache add gcc libc-dev libffi-dev openssl-dev bsd-compat-headers libmagic libxslt-dev

# Upgrade pip to the latest.
RUN pip install --upgrade pip
RUN pip install --no-cache-dir -r requirements.txt
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
