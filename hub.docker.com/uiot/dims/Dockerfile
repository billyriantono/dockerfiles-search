FROM python:3.7

ENV MONGODB_URI="mongodb://mongo:27017" \
    ENV="DOCKER"

WORKDIR /usr/src/app

COPY setup.py README.md ./
COPY dims/__init__.py ./dims/__init__.py

RUN pip install -e .

COPY . .

ENTRYPOINT ["uwsgi", "--ini", "uwsgi.ini"]
