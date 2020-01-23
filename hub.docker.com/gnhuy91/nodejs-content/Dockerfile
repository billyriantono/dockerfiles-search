FROM schmich/armv7hf-alpine-qemu
LABEL maintainer "gustavo.michels@gmail.com"

RUN ["cross-build-start"]

RUN apk --update add python2 py-pip && \
    rm -fr /var/cache/apk

RUN pip install pytz requests

RUN ["cross-build-end"]

ADD dnsomatic.py /

ENTRYPOINT ["/usr/bin/python", "-u", "/dnsomatic.py"]
