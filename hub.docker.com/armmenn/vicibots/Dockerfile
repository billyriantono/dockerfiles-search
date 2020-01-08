FROM python:2.7
ENV PYTHONUNBUFFERED 1
RUN mkdir /code
WORKDIR /code
# follwoing two lines are for cloning deps from bitbucket
RUN mkdir ~/.ssh
RUN ssh-keyscan -t rsa bitbucket.org > ~/.ssh/known_hosts
#
ADD requirements.txt /code/requirements.txt
RUN pip install -r requirements.txt
ADD . /code/
ENV DJANGO_SETTINGS_MODULE vicibots.prod_settings
# use only in autobuilds
RUN python manage.py collectstatic --noinput