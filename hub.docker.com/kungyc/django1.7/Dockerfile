FROM kungyc/python3:v150708

MAINTAINER kungyc Django1.7 Virtualenv

RUN apt-get update
RUN apt-get install -y python-virtualenv
RUN pip install "django<1.8"

WORKDIR /home

EXPOSE 80

EXPOSE 8000 
