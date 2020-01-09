FROM frolvlad/alpine-python2:latest

ENV server http://localhost:6800

RUN pip install spiderkeeper
RUN apk update
RUN apk add tzdata
RUN cp /usr/share/zoneinfo/Asia/Hong_Kong /etc/localtime
RUN echo "Asia/Hong_Kong" > /etc/timezone

ENTRYPOINT ["spiderkeeper"]

EXPOSE 5000
