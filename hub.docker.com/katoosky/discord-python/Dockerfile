FROM python:3.7.3-alpine3.9

LABEL maintainer="かとまさ <katomasa@kidding-kid.com>" \
      version="1.0.1" \
      description="Python container for Discord Bot." \
      registry="dockerhub" \
      app="discord"

# ここから独自のコード
COPY Pipfile ./
COPY Pipfile.lock ./
RUN apk update && \
    apk add postgresql-libs && \
    apk add --virtual .build-deps gcc musl-dev postgresql-dev && \
    pip install pipenv && \
    pipenv install --system && \
    apk --purge del .build-deps

CMD [ "tail", "-f", "/dev/null"]