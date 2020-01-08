FROM django

MAINTAINER amanoese

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

ONBUILD COPY . /usr/src/app
# install module
RUN pip install django-http-proxy

EXPOSE 8000
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
