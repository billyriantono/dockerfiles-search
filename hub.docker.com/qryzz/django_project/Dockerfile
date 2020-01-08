FROM ubuntu:14.04
RUN apt-get update
RUN apt-get -y upgrade
RUN apt-get install -y nginx
RUN apt-get install -y python3-pip
RUN pip3 install virtualenv
RUN virtualenv /home/venv
RUN . /home/venv/bin/activate && pip3 install django && pip3 install djangorestframework && pip3 install uwsgi && pip3 install gunicorn && apt-get install -y gunicorn
RUN apt-get install -y git
RUN apt-get update
RUN apt-get -y upgrade
RUN git clone https://grechko@bitbucket.org/grechko/intro-projects.git
RUN . /home/venv/bin/activate && python intro-projects/QUIZ/manage.py collectstatic