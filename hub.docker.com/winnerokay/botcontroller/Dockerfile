FROM tiangolo/meinheld-gunicorn:python3.6-alpine3.8 as base

FROM base as builder

RUN mkdir /install
RUN apk update && apk add postgresql-dev gcc python3-dev musl-dev
WORKDIR /install
COPY ./app/requirements.txt /requirements.txt
RUN pip install --install-option="--prefix=/install" -r /requirements.txt

FROM base

COPY --from=builder /install /usr/local
COPY app /app
RUN apk --no-cache add libpq
RUN apk add bash
WORKDIR /app