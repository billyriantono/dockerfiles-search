FROM gliderlabs/alpine:3.1
MAINTAINER Chris George <chris.a.george at gmail.com>
RUN apk --update add python py-pip && mkdir /app && rm -rf /var/cache/apk/* && pip install "devpi-server>=2.0.6,<2.1dev" "devpi-client>=2.0.2,<2.1dev" \
        "requests>=2.4.0,<2.5"
VOLUME /app
EXPOSE 3141
ADD run.sh /app/
CMD sh /app/run.sh

