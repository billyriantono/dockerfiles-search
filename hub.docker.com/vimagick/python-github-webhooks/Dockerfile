#
# Dockerfile for python-github-webhooks
#

FROM alpine
MAINTAINER "Laurent Rineau" <laurent.rineau@cgal.org>

ADD LICENSE requirements.txt webhooks.py config.json /src/

RUN apk add -U py-pip \
    && rm -rf /var/cache/apk/* \
    && pip install -r /src/requirements.txt

VOLUME /src/hooks
EXPOSE 5000
WORKDIR /src

CMD ["python", "webhooks.py"]
