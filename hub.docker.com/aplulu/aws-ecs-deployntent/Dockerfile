FROM python:alpine
LABEL maintainer "Michael Henke <433270+aphex3k@users.noreply.github.com>"
RUN apk add jpeg-dev git zlib-dev gcc musl-dev

RUN mkdir -p /app
RUN mkdir -p /data

RUN git clone --depth=1 https://github.com/aphex3k/sonos-slack.git /app
RUN pip3 install -r /app/requirements.txt

WORKDIR /data/

ENV GOOGLE_API_TOKEN ""
ENV GOOGLE_CX_TOKEN ""
ENV SLACK_API_TOKEN ""

ENTRYPOINT ["python", "/app/sonos-slack.py"]
