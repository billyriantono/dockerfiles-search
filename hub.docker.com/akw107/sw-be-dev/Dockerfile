FROM python:3.5
MAINTAINER A.K. Williams <akwillia2@gmail.com>
USER root

# install nginx x for serving the static files & create conf dir if it doect' exist
#RUN apt-get update && apt-get install -y nginx
#RUN if ! [ -d /etc/nginx/conf.d ]; then mkdir -p /etc/nginx/conf.d; fi;

#create gunicorn access and error logs
RUN mkdir -p /var/log/gunicorn/
RUN touch /var/log/gunicorn/gunicorn.log
RUN touch  /var/log/gunicorn/gunicorn-access.log

## install supervisor and overwrite the supervisor conf file
#RUN apt-get update && apt-get install -y supervisor
#RUN rm /etc/supervisor/supervisord.conf
#COPY  [...]  /etc/supervisor/supervisord.conf

RUN pip3 install --upgrade pip
# set the django environment to the dev env

RUN mkdir -p /backend_code

WORKDIR /backend_code

COPY  requirements.txt /backend_code/
RUN pip install -r requirements.txt
COPY . /backend_code/

EXPOSE 8080
#EXPOSE 80
CMD ["gunicorn", "--workers",  "3", "--bind",  "localhost:8001",   "sw_backend.wsgi:application"]
#CMD ["python", "manage.py", "runserver", "0.0.0.0:80"]