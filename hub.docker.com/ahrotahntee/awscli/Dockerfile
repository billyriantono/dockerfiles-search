FROM alpine:latest
RUN apk add --update python curl jq groff py2-pip
WORKDIR /root
RUN pip install --upgrade pip && pip install botocore awscli
ENTRYPOINT ["/usr/bin/aws"]
