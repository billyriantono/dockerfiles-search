FROM python:2-alpine

RUN apk update \
    && apk add --no-cache gcc linux-headers musl-dev libffi-dev openssl-dev libxslt-dev \
    && pip install octodns==0.9.3 azure-common==1.1.9 msrestazure==0.4.27 azure-mgmt-dns==1.0.1 boto3==1.7.5 dyn==1.8.1

CMD /bin/sh
