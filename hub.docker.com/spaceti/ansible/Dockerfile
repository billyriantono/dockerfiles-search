FROM python:3.6.4-alpine3.4
LABEL maintainer: "Sergey Shkarupa <s.shkarupa@gmail.com>"

RUN apk --no-cache add --virtual .build-deps libffi-dev openssl-dev build-base && \
    apk --no-cache add make openssh-client && \
    pip install -U --no-cache-dir --disable-pip-version-check ansible && \
    apk --no-cache del .build-deps

CMD ["ansible-playbook", "--version"]
