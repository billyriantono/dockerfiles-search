FROM alpine:latest

RUN apk upgrade --update && \
    apk add --update --no-cache python3 curl ca-certificates bash tar git openssh tzdata && \
    if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi && \
    if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi && \
    pip install --no-cache awscli boto3

CMD /bin/bash
