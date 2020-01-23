FROM python:3.5
ENV PYTHONUNBUFFERED 1

MAINTAINER Andrew Marconi <andrew@559labs.com>

USER root
RUN apt-get update; apt-get -y upgrade

RUN mkdir -p /code
WORKDIR /code
ADD ./code /code/
RUN pip install -r /code/requirements.txt
RUN python manage.py migrate

EXPOSE 8000

ENTRYPOINT ["python", "manage.py", "runserver_plus", "0.0.0.0:8000"]
