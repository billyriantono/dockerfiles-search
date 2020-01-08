FROM ubuntu:14.10

MAINTAINER Andrés Sánchez García

RUN apt-get update &&\
    apt-get upgrade -y &&\
    apt-get install -y python-pip libpq-dev python-dev git &&\
    apt-get clean &&\
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


ADD requeriments.txt /tmp/
RUN pip install -r /tmp/requeriments.txt &&\
    mkdir /srv/app &&\
    git clone https://github.com/asg1612/django-testdocker.git /srv/app/


EXPOSE 8000

WORKDIR /srv/app/django-testdocker/
CMD ["/usr/bin/python3.4", "manage.py", "runserver", "0.0.0.0:8000"]
