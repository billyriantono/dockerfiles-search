FROM python:3.7.4-buster

LABEL MAINTAINER="Duc Vo Ngoc <development@donkz.dev>"

ENV GROUP_ID=1000 \
    USER_ID=1000

WORKDIR /var/www

RUN pip install pipenv
COPY Pipfile Pipfile.lock /var/www/
RUN pipenv install

ADD . /var/www

RUN pip install gunicorn

RUN groupadd -g $GROUP_ID www
RUN useradd -u $USER_ID -g www www -s /bin/sh

USER www

EXPOSE 8888

CMD [ "gunicorn", "-w", "4", "--bind", "0.0.0.0:8888", "wsgi"]