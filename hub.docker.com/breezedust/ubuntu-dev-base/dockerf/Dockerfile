FROM python:3.7-alpine

COPY Pipfile /Pipfile

RUN apk add --no-cache --virtual .build-deps gcc libc-dev make \
 && pip install pipenv \
 && pipenv install --system --skip-lock \
 && apk del .build-deps gcc libc-dev make

COPY src /src

EXPOSE 5000

ENTRYPOINT [ "python", "src/__main__.py" ]