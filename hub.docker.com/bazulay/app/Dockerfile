FROM fedora:27

MAINTAINER bazulay@gmail.com

RUN dnf update -y && dnf install -y procps-ng net-tools psmisc 
RUN dnf install -y supervisor
#adding appuser  user & group to avoid running as root
RUN groupadd -g 1234 appuser && useradd -r -u 1234 -g 1234 -m  appuser

#Declaring the workdir
WORKDIR /app

#Adding the application files to the image , and creating necessary directories
ADD app/  /app
RUN mkdir /app/logs /app/db /app/run  

#Chowning all files we have added  before switching to appuser
RUN chown -R appuser:appuser /app

USER appuser

#installing all necessary python packages
RUN pip3 install --user  inotify flask python-dotenv flask-socketio \
    python-dateutil flask-sqlalchemy flask-migrate



#define the volume onto we mount the relevant hostfiles
VOLUME ["/logs"]

ENV FLASK_APP app.py

EXPOSE 5000

CMD /usr/bin/supervisord -n  -c /app/etc/supervisord.conf
