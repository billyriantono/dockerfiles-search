FROM python:alpine

RUN apk update \
  && apk upgrade \
  && apk add --no-cache git git-lfs openssh

RUN pip install github-backup

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
VOLUME /usr/src/app

ENTRYPOINT ["github-backup"]
CMD ["--help"]
