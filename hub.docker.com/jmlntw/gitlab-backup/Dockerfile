FROM python:alpine

RUN apk update \
  && apk upgrade \
  && apk add --no-cache git git-lfs openssh

RUN pip install gitlab-backup

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
VOLUME /usr/src/app

ENTRYPOINT ["gitlab-backup"]
CMD ["--help"]
