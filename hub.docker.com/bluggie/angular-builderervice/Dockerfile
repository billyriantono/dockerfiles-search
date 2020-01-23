FROM ubuntu:17.10
MAINTAINER Ference van Munster: 0.0.1

RUN apt-get clean
RUN apt-get update --fix-missing
RUN apt-get install -y python3-setuptools python3-pip python3-dev python3 build-essential
#RUN apt-get install -y libffi-dev libssl-dev libmemcached-dev
#RUN apt-get install -y gettext
#RUN apt-get install -y zip unzip
#RUN apt-get install -y libjpeg8 libjpeg62-dev libfreetype6 libfreetype6-dev
#RUN apt-get install -y locales

#RUN locale-gen en_US.UTF-8
#ENV LANG en_US.UTF-8
#ENV LANGUAGE en_US:en
#ENV LC_ALL en_US.UTF-8

ENV PYTHONUNBUFFERED 1

ENV DJANGO_SETTINGS_MODULE application.settings

WORKDIR /

RUN mkdir -p /data
RUN mkdir -p /data/blue_landscape
RUN mkdir -p /data/blue_landscape/natural_language_processing_service/
RUN mkdir -p /data/blue_landscape/natural_language_processing_service/media
RUN chmod 777 -R /data/blue_landscape/natural_language_processing_service/media

RUN mkdir -p /data/blue_landscape/natural_language_processing_service/application
RUN mkdir -p /data/blue_landscape/natural_language_processing_service/models

ADD ./ /data/blue_landscape/natural_language_processing_service/application

RUN mkdir -p /data/blue_landscape/natural_language_processing_service/static
RUN chmod 777 -R /data/blue_landscape/natural_language_processing_service/static

RUN pip3 install virtualenv

# Install application requirements
RUN virtualenv /data/blue_landscape/natural_language_processing_service/venv/
RUN /data/blue_landscape/natural_language_processing_service/venv/bin/pip3 install -r /data/blue_landscape/natural_language_processing_service/application/requirements.txt --upgrade

# Download spacy libraries
RUN /data/blue_landscape/natural_language_processing_service/venv/bin/python -m spacy download en
RUN /data/blue_landscape/natural_language_processing_service/venv/bin/python -m spacy download de
RUN /data/blue_landscape/natural_language_processing_service/venv/bin/python -m spacy download es
RUN /data/blue_landscape/natural_language_processing_service/venv/bin/python -m spacy download pt
RUN /data/blue_landscape/natural_language_processing_service/venv/bin/python -m spacy download fr
RUN /data/blue_landscape/natural_language_processing_service/venv/bin/python -m spacy download it
RUN /data/blue_landscape/natural_language_processing_service/venv/bin/python -m spacy download nl
RUN /data/blue_landscape/natural_language_processing_service/venv/bin/python -m spacy download xx

EXPOSE 8000 8080
CMD ["bash", "/data/blue_landscape/natural_language_processing_service/application/docker/application/run.sh"]
