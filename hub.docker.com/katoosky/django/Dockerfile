FROM python:3.7.3-alpine3.9

LABEL maintainer="かとまさ <katomasa@kidding-kid.com>" \
      version="1.0.4" \
      description="Python container for Django Application." \
      registry="dockerhub" \
      app="django"

# ここから独自のコード
COPY Pipfile ./
COPY Pipfile.lock ./
RUN apk update && \
    apk add --virtual .build-deps gcc musl-dev mariadb-dev && \
    pip install pipenv && \
    pipenv install --system
    # apk --purge del .build-deps

WORKDIR /app

CMD [ "tail", "-f", "/dev/null"]