FROM python:alpine
LABEL maintainer="Daniel Winks"

WORKDIR /usr/src/app

COPY . .

RUN apk add --no-cache bash gcc musl-dev &&  rm -rf /var/cache/apk/*

RUN pip3 install --upgrade pip; pip3 install --no-cache-dir -e .

COPY .bashrc /root/.bashrc

ENTRYPOINT ["hass-cli"]
