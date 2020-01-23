FROM python:3.7
MAINTAINER Dongeon Kim <kde713@gmail.com>

RUN pip install pipenv

RUN set -ex && mkdir /app
WORKDIR /app

COPY iamport_mock iamport_mock
COPY Pipfile Pipfile
COPY Pipfile.lock Pipfile.lock

RUN pipenv install

ENTRYPOINT ["pipenv", "run"]
CMD ["python", "-m", "iamport_mock"]