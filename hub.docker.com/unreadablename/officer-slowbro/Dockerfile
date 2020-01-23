FROM alpine:latest
RUN apk add --no-cache \
        python \
        py-pip \
        groff \
        less \
        mailcap \
        && \
    pip install --upgrade --no-cache-dir \
      pip \
      setuptools &&\
    pip install --upgrade --no-cache-dir \
      awscli s3cmd python-magic python-dateutil &&\
    apk -v --purge del py-pip

VOLUME ["/root/.aws"]
WORKDIR /work

CMD ["aws"]
