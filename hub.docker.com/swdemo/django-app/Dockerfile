FROM python:3
MAINTAINER Alexis

RUN groupadd -r django && useradd -r -g django django

RUN pip3 install --no-cache-dir uwsgi django mysqlclient

COPY uwsgi.ini admin.py models.py settings.py migrate.sh /home/django/

RUN mkdir -p /home/django/website/model_example/ && chown -R django:django /home/django

USER django
WORKDIR /home/django

RUN  django-admin startapp model_example /home/django/website/model_example/

RUN mv admin.py website/model_example/ && \
    mv models.py website/model_example/ && \
    django-admin startproject website /home/django/website &&\
    mv settings.py website/website/ && \
    echo yes | python3 website/manage.py collectstatic
#RUN echo "from django.contrib.auth.models import User; User.objects.create_superuser('admin', 'admin@example.com', '$DJANGO_ADMIN_PASSWORD')" | python3 /home/django/website/manage.py shell

EXPOSE 8008

CMD ["/usr/local/bin/uwsgi", "--ini", "uwsgi.ini"]
