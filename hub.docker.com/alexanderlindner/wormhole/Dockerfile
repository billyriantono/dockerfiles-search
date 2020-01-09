FROM python:3.6-alpine
MAINTAINER Alexander Lindner <25225552+alexander-lindner@users.noreply.github.com>

WORKDIR /data

RUN apk add --virtual  .build-deps gcc freetype-dev musl-dev  libffi-dev openssl-dev make && pip install magic-wormhole && apk del .build-deps gcc freetype-dev musl-dev  libffi-dev openssl-dev make

ENTRYPOINT ["wormhole"]

ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8
