FROM alpine:latest

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="dgg-stats" \
      org.label-schema.description="Python application to track emote usage in Destiny.GG chatroom" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/ChristopherJHart/dgg-stats" \
      org.label-schema.schema-version="1.0"

RUN apk --update --no-cache add python3-dev gcc g++
RUN pip3 install --upgrade pip
RUN mkdir /dgg-stats
ADD requirements.txt /dgg-stats/requirements.txt
RUN pip3 install -r /dgg-stats/requirements.txt
ADD . /dgg-stats
CMD ["python3", "-u", "/dgg-stats/dgg_stats.py"]