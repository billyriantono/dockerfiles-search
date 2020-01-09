FROM ubuntu:16.04
MAINTAINER Vindula <contato@vindula.com.br>

# Criando o diretorio do Vindula
RUN mkdir -p /vindula/vindulanext
WORKDIR /vindula/vindulanext

# Copiando o codigo-fonte
ADD . /vindula/vindulanext

## Instando as dependencias do Vindula
RUN apt-get -yqq update && apt-get -yqq install python3 python3-dev python3-pip libreoffice swig libxml2-dev libxslt1-dev antiword unrtf locales poppler-utils pstotext tesseract-ocr flac lame libpulse-dev libmad0 libsox-fmt-mp3 sox libjpeg-dev supervisor build-essential python-dev libldap2-dev libsasl2-dev ldap-utils ffmpeg gettext

# Ajustando Locale
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Instalando os pacotes do Vindula
RUN pip3 install --upgrade pip setuptools
RUN pip install -r requirements.txt
RUN pip install uwsgi psycopg2-binary python-ldap django-auth-ldap python-dateutil django-extensions django-import-export django_select2==6.3.1 pyexcel pyexcel-xlsx pyexcel-xls icalendar superjson django-picklefield django_qr_code djangorestframework djangorestframework_simplejwt django-msgpackfield django_redis mysql-connector-python django-rosetta

# Configurando o supervisor para o celery
RUN mkdir -p /var/log/supervisor
RUN mkdir -p /var/log/celery
RUN touch /var/log/celery/vindulanext_beat.log && touch /var/log/celery/vindulanext_worker.log
COPY confs/supervisor_celery_beat.conf /etc/supervisor/conf.d/supervisor_celery_beat.conf
COPY confs/supervisor_celery_worker.conf /etc/supervisor/conf.d/supervisor_celery_worker.conf
CMD ["/usr/bin/supervisord"]







