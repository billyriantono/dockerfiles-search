FROM python:3.6-alpine3.6

RUN apk --no-cache add build-base tar musl-utils openssl-dev linux-headers openssl-dev libssl1.0 gcc libffi py-cffi python-dev libffi-dev py-openssl curl bash jq \
    && ln -s /lib/libc.musl-x86_64.so.1 ldd \
    && ln -s /lib /lib64 \
    && pip3 install setuptools cx_Freeze==6.0b1 requests-aws4auth boto3 elasticsearch-curator==5.5.4 \
    && apk del gcc python-dev libffi-dev musl-dev linux-headers openssl-dev

ADD resources/ /resources
USER nobody:nobody

ENTRYPOINT ["/usr/bin/curator"]
