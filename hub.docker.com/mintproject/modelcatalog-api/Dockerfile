FROM python:3-alpine

RUN apk add --no-cache build-base openssl-dev libffi-dev python-dev alpine-sdk mariadb-connector-c mariadb-connector-c-dev
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY Pipfile /usr/src/app
COPY Pipfile.lock /usr/src/app

RUN pip install pipenv
RUN pipenv install --deploy --system

COPY . /usr/src/app

EXPOSE 8080

CMD ["sh", "init.sh"]
