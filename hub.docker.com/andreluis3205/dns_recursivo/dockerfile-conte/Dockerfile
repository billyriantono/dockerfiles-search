FROM jrottenberg/ffmpeg:4.1-alpine

MAINTAINER Andreas Fies <andreas.richard@fiese.info>

ARG VCS_REF
ARG BUILD_DATE

LABEL org.label-schema.name="FFProcess" \
      org.label-schema.description="A small docker container including ffmpeg to batch convert your media library to a defined h264/aac profile for better compatibility for PS4. " \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-url="https://github.com/andreasrichardf/ffprocess"

ADD ffprocess.py /usr/local/bin/ffprocess.py
ADD requirements.txt /tmp/requirements.txt

RUN apk add --no-cache -U \
  alpine-sdk \
  bash \
  python3 \
  python3-dev \
  tini \
  && pip3 install -r /tmp/requirements.txt \
  && rm -f /tmp/requirements.txt \
  && apk del \
  alpine-sdk \
  python3-dev

VOLUME /data

ENTRYPOINT ["/sbin/tini", "--", "python3", "/usr/local/bin/ffprocess.py", "/data"]
