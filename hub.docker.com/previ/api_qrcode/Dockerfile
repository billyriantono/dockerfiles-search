FROM ubuntu:latest

MAINTAINER Roberto Previtera <roberto.previtera@gmail.com>

RUN apt-get update
RUN apt-get -y install libjpeg8-dev libtiff5-dev libjasper-dev libpng12-dev libjpeg-dev
RUN apt-get -y install python-pip python-dev

RUN pip install Flask
RUN pip install flask-cors
RUN pip install Pillow
RUN pip install qrcode

RUN mkdir /appl \
    mkdir /appl/api_qrcode

COPY . /appl/api_qrcode

EXPOSE 5000

CMD ["python", "/appl/api_qrcode/api.py"]
