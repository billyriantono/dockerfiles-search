FROM python:3.6-alpine3.7

COPY . .

RUN apk add --no-cache git gcc musl-dev postgresql-dev python3-dev \
 && pip3 install pipenv \
 && pip3 install Jinja2 \
 && pipenv install --system --deploy \
 && apk del git gcc musl-dev python3-dev

CMD python src/main.py
