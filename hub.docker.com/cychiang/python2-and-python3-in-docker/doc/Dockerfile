FROM gliderlabs/alpine:3.2

RUN apk add --update \
    python3 \
    python3-dev \
    py-pip \
    build-base \
    curl \
  && pip install virtualenv \
  && rm -rf /var/cache/apk/*

WORKDIR /app

ONBUILD COPY . /app
ONBUILD RUN virtualenv -p /usr/bin/python3 /env && /env/bin/pip install -r /app/requirements.txt

CMD ["/env/bin/python3", "main.py"]
