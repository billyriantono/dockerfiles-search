# Python support can be specified down to the minor or micro version
# (e.g. 3.6 or 3.6.3).
# OS Support also exists for jessie & stretch (slim and full).
# See https://hub.docker.com/r/library/python/ for all supported Python
# tags from Docker Hub.
FROM python:alpine

LABEL Name=eagle-api author="蒋瞿风"

COPY . /app
WORKDIR /app

ENV FLASK_APP=app.py
ENV PIPENV_VENV_IN_PROJECT=1

RUN python3 -m pip install pipenv
RUN pipenv install --system --deploy

EXPOSE 5000

CMD ["python", "-m", "flask", "run", "--host=0.0.0.0"]

