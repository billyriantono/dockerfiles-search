FROM python:3.7-alpine3.8

ENV LC_ALL C.UTF-8
ENV LANG C.UTF-8
ENV USER=pipenv
ENV UID=9123
ENV GID=9123
ENV WORKDIR=/app

RUN pip3 install --upgrade pip setuptools && \
    pip3 install pipenv

WORKDIR "$WORKDIR"

ONBUILD COPY Pipfile Pipfile
ONBUILD COPY Pipfile.lock Pipfile.lock

ONBUILD RUN set -ex && pipenv install --deploy --system

ONBUILD RUN addgroup --system --gid "$GID" "$USER" \
            && adduser \
            --disabled-password \
            --gecos "" \
            --home "$WORKDIR" \
            --ingroup "$USER" \
            --no-create-home \
            --uid "$UID" \
            --system "$USER"

ONBUILD USER "$USER"
