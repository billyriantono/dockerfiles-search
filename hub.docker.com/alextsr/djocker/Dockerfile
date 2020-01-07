# To be run mounting the Django project dir to /srv
# i.e. docker run -d -p 8080 -v $PWD:/srv alextsr/djoker

FROM ubuntu

MAINTAINER Alexandros Tsourakis, alex.tsr@gmail.com

RUN apt-get update ; apt-get install -y python3-setuptools
RUN easy_install3 pip
RUN pip3 install django

EXPOSE 8080

CMD ["python3", "/srv/manage.py", "runserver", "0.0.0.0:8080"]
