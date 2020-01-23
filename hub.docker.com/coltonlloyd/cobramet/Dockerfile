# Dockerfile para la imagen de la aplicacion django de  #
# que sirve la pagina web de la SPGO.                   #
#-------------------------------------------------------#
# Variables de entorno necesarias:                      #
#   1) SPGO_SERVICE_DOMAIN (Ej.http://134.209.15.20:81) #
#-------------------------------------------------------#

FROM python:3.5.6-stretch
ENV PYTHONUNBUFFERED 0
ENV C_FORCE_ROOT true
RUN mkdir /src
RUN mkdir /static
WORKDIR /src
ADD . /src
ADD ./pagina_web/static /static
# Dependencias de python
RUN pip install -r requirements.txt
CMD python manage.py makemigrations && python manage.py migrate --run-syncdb; sh start-gunicorn.sh;
