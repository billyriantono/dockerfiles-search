FROM alpine:3.6

RUN apk add --no-cache python3=3.6.1-r3 && \
    pip3 install Django==1.11.6 && \
    django-admin startproject quickstart

RUN cd /quickstart && \
    sed -i "s/ALLOWED_HOSTS = \[\]/ALLOWED_HOSTS = ['*']/" quickstart/settings.py

WORKDIR /quickstart

EXPOSE 80

CMD ["python3.6", "manage.py", "runserver", "0.0.0.0:80"]
