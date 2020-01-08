FROM ubuntu:12.04

COPY . /src

RUN cd /src && apt-get update && apt-get build-dep -y python-psycopg2 && apt-get install -y python-pip && pip install -r requirements.txt && rm -rf /var/lib/apt/lists/*

CMD cd /src && python manage.py syncdb --all --noinput && python manage.py migrate --fake && python setup_demo_user.py && python manage.py runserver 0.0.0.0:$PORT
