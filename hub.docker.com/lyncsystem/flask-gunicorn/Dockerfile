FROM python:3.7-alpine as base

# working directory
WORKDIR /app

# copy current directory into the container
ADD app /app

# install requirements
RUN pip3 install pipenv && set -ex && pipenv install --deploy --system

VOLUME /app

# make port 8000 available to the world outside
EXPOSE 8000

CMD ["gunicorn", "--config", "./conf/gunicorn_config.py", "server:app"]