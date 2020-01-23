FROM debian:stretch

RUN apt-get update -y && apt-get upgrade -y
RUN apt-get install -y python-pip
#RUN pip install textwrap

RUN mkdir -p /var/www/
COPY ./dicoweb /var/www/dicoweb
WORKDIR /var/www/dicoweb

#RUN virtualenv venv
#RUN . venv/bin/activate
RUN pip install -r requirements.txt
#RUN ./venv/bin/deactivate

ENTRYPOINT ["/bin/bash", "-c", "python manage.py runserver 0.0.0.0:8000"]
