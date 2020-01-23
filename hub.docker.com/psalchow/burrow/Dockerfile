FROM ubuntu:latest

MAINTAINER Roberto Previtera <roberto.previtera@gmail.com>

RUN apt-get -y update
RUN apt-get -y upgrade 
RUN apt-get -y install wget zlib1g-dev libxml2-dev libxslt1-dev python-pip python-dev python3-lxml

RUN pip install --upgrade pip
RUN pip install Flask
RUN pip install flask-cors
RUN pip install zeep
RUN pip install python-jose

WORKDIR /tmp/downloads

RUN mkdir /appl && \
    mkdir /appl/api_nemos

COPY . /appl/api_nemos

EXPOSE 5000

CMD ["python", "/appl/api_nemos/api.py"]
