FROM amd64/alpine:3.10.1
LABEL Description="Home Assistant"

ARG UID=1000
ARG GUID=1000

RUN apk add --no-cache git python3 ca-certificates libffi-dev openssl-dev bash curl openssl ffmpeg && \
    addgroup -g ${GUID} hass && \
    adduser -h /data -D -G hass -s /bin/sh -u ${UID} hass && \
    pip3 install --upgrade --no-cache-dir pip && \
    apk add --no-cache --virtual=build-dependencies build-base linux-headers python3-dev tzdata

COPY requirements.txt requirements.txt
COPY ssl-cert-check /bin/

RUN pip3 install --no-cache-dir -r requirements.txt

RUN apk del build-dependencies && \
    rm -rf /tmp/* /var/tmp/* /var/cache/apk/* && \
    rm requirements.txt && \
    chmod +x /bin/ssl-cert-check 

EXPOSE 8123

ENTRYPOINT ["hass", "--open-ui", "--config=/data"]
