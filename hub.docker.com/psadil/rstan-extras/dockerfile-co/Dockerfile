FROM ubuntu:latest

MAINTAINER Roberto Previtera <roberto.previtera@gmail.com>

RUN apt-get update
RUN apt-get -y install python-pip python-dev

RUN pip install Flask
RUN pip install flask-cors
RUN pip install python-jose

RUN mkdir /appl \
    mkdir /appl/api_auth

COPY . /appl/api_auth

EXPOSE 5000

CMD ["python", "/appl/api_auth/api.py"]
