FROM ubuntu:14.04
RUN apt-get update
RUN apt-get -y install python-pip
RUN pip install django
RUN pip install djangorestframework
ADD ./ /opt/django-sample/
WORKDIR /opt/django-sample
EXPOSE 8080
CMD ["python", "manage.py", "runserver", "0.0.0.0:8080"]