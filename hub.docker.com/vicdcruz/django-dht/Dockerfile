# Standardization of a universal version
FROM python:3.6

# Environment For PIPENV
ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8=value

# Basic updating
RUN apt update

# DJango
RUN pip install Django
RUN django-admin --version

# Dev tools for MySQL feat. Python
RUN apt install mysql-server -y
RUN apt install python-dev -y

# PipEnv
RUN pip install pipenv
RUN pip install djangorestframework
RUN pip install django-cors-headers
# RUN pipenv shell
# RUN pipenv install
# RUN ./manage.py runserver

# Git
RUN apt install git -y
RUN git --version
RUN git config --global user.name "Victor Cruz"
RUN git config --global user.email "victor.cruz@dhtmexico.com"

EXPOSE 8000