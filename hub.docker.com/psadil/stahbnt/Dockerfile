FROM previ/openbr:latest

MAINTAINER Roberto Previtera <roberto.previtera@gmail.com>

RUN apt-get -y install libjpeg8-dev libtiff4-dev libjasper-dev libpng12-dev libjpeg-dev

RUN pip install Flask
RUN pip install flask-cors
RUN pip install Pillow

RUN mkdir /appl \
    mkdir /appl/apicvbr

COPY . /appl/apicvbr

EXPOSE 5000

CMD ["python", "/appl/apicvbr/api.py"]
