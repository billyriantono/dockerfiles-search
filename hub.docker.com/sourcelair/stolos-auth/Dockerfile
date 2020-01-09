FROM python:3.5.2
MAINTAINER Antonis Kalipetis <akalipetis@gmail.com>

COPY . /opt/stolos-auth
WORKDIR /opt/stolos-auth
RUN python setup.py install

ENTRYPOINT ["stolos-auth"]
