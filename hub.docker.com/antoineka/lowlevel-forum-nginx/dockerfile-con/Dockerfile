FROM docker:dind

LABEL maintainer="Andrey Voronkov <avoronkov@enapter.com>"

RUN set -x \
  && apk --no-cache add python python-dev py-pip build-base libffi-dev openssl-dev libgcc \
  && pip install docker-compose
