FROM python:3.6.6-slim

RUN \
    apt-get update && \
    apt-get install -y --no-install-recommends git && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /code

RUN pip install pipenv

ADD Pipfile .
ADD Pipfile.lock .
RUN pipenv install --system --deploy

ADD . /code
CMD ["python", "manage.py"]
