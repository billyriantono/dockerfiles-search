FROM ubuntu:16.04

WORKDIR .
COPY requirements.txt ./
COPY ./examenes /var/www/html/examenesmonolitico/examenes
COPY ./examenes/_datos_iniciales/settings_inicial.py /var/www/html/examenesmonolitico/examenes/examenes/settings.py
COPY ./examenes/_datos_iniciales/secrets_inicial.json /var/www/html/examenesmonolitico/examenes/secrets.json

RUN echo "nameserver 172.18.0.1" >> /etc/resolv.conf && apt-get update && apt-get install -y --no-install-recommends apache2 apache2-utils python3 python3-setuptools libapache2-mod-wsgi-py3 python3-pip && rm -rf /var/lib/apt/lists/* && ln /usr/bin/python3 /usr/bin/python && ln /usr/bin/pip3 /usr/bin/pip
RUN echo "nameserver 172.18.0.1" >> /etc/resolv.conf && pip install --upgrade pip
RUN echo "nameserver 172.18.0.1" >> /etc/resolv.conf && pip install -r requirements.txt

COPY ./examenes/_datos_iniciales/apache-conf.conf /etc/apache2/sites-available/000-default.conf

RUN mkdir -p /var/www/html/examenesmonolitico/media
VOLUME /var/www/html/examenesmonolitico/media

RUN echo yes | python /var/www/html/examenesmonolitico/examenes/manage.py collectstatic && rm -rf /var/www/html/examenesmonolitico/examenes/static
EXPOSE 80 8080
CMD ["apache2ctl", "-D", "FOREGROUND"]
