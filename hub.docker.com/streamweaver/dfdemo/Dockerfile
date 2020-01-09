FROM python:3-alpine
MAINTAINER Scott Turnbull "scott.turnbull@us-ignite.org"

RUN pip install Flask requests

VOLUME /opt/flaskapp
EXPOSE 5000

COPY . /opt/flaskapp

ENV FLASK_APP_NAME "Using Dockerfiles Ep4"

WORKDIR /opt/flaskapp
CMD ["python", "run.py"]
