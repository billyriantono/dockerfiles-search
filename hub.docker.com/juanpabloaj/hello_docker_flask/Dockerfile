from python:2-alpine

RUN pip install flask gunicorn

ADD . /app
WORKDIR /app

ENTRYPOINT ["gunicorn", "app:app"]
