
FROM python:3.6

WORKDIR /usr/src/app

RUN pip install pipenv --no-cache-dir

ADD Pipfile /usr/src/app
ADD Pipfile.lock /usr/src/app
RUN pipenv install

ADD . /usr/src/app
RUN mkdir -p /usr/src/app/logs/ && \
    pipenv run python manage.py collectstatic --noinput

ENTRYPOINT ["pipenv", "run", "gunicorn", "vcob.wsgi", "-c", "./etc/gunicorn.py"]
