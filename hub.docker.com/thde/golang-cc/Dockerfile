FROM golang:jessie

RUN apt-get update && apt-get install -y --no-install-recommends \
    zip \
    && rm -rf /var/lib/apt/lists/*

COPY cc /usr/local/bin/

ENV APP_PATH /go/src/app
ENV MAKEFILE_PATH /usr/local/share/Makefile
ENV APP_NAME app

COPY Makefile ${MAKEFILE_PATH}

WORKDIR ${APP_PATH}

CMD [ "cc" ]
