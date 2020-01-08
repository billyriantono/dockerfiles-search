# Dockerfile

#Start with a Python image
FROM python:latest

MAINTAINER Tomasz Sapletta <tomasz@sapletta.com>

# EXPOSE port to allow communication to/from server
EXPOSE 8080

ADD . /zamowienia

ENV DJANGO_SETTINGS_MODULE zamowienia.settings

RUN pip install -r /zamowienia/requirements.txt

RUN python /zamowienia/manage.py collectstatic --noinput

CMD python /zamowienia/manage.py runserver 0.0.0.0:8080