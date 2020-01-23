FROM alpine

WORKDIR /python

ADD . /python

RUN apk --no-cache add python

CMD python -m SimpleHTTPServer 8080

EXPOSE 8080
