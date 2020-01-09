FROM alpine:latest
MAINTAINER playniuniu@gmail.com

COPY app/ /usr/src/app/
COPY requirements.txt /usr/src/

WORKDIR /usr/src/

RUN apk --no-cache --update add python3 \
    && python3 -m venv env \
    && ./env/bin/pip install --upgrade pip \
    && ./env/bin/pip install -r requirements.txt \
    && rm -r /var/cache/apk/*

EXPOSE 8000
CMD ["./env/bin/gunicorn", "-b", "0.0.0.0:8000", "app:app"]
