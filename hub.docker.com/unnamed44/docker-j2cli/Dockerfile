FROM alpine

RUN apk update \
 && apk add --no-cache py2-pip \
 && pip install --upgrade pip \
 && pip install j2cli

WORKDIR /

ENTRYPOINT ["j2"]

CMD ["--help"]
