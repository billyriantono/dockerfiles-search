FROM python:3.7.4-alpine3.10

LABEL MAINTAINER eric4545@gmail.com

WORKDIR /app

RUN mkdir -p /app && \
    apk add --no-cache --update \
        g++ \
        zeromq-dev \
    && \
    pip3 install \
        pipenv \
        Cython

COPY ["Pipfile","Pipfile.lock","./"] .

RUN apk --no-cache add --virtual=.build-dep \
        build-base \
    && \
    pipenv install \
        --deploy \
        --system \
        --three \
    && \
    apk del .build-dep

COPY . .

EXPOSE 8089 5557 5558

ENTRYPOINT [ "locust" ]
