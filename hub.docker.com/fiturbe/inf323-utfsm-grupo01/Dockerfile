# Se toma como imagen base alpine
FROM python:3.5-alpine

# Se copia el archivo de requerimientos a /requirements.txt del container (ruta absoluta del container)
ADD requerimientos.txt /requirements.txt

# Se instalan las dependencias, luego 'pip', finalmente se remueve lo innecesario que haya sido generado durante este proceso.
RUN set -ex \
    && apk add --no-cache --virtual .build-deps \
            gcc \
            make \
            libc-dev \
            musl-dev \
            linux-headers \
            pcre-dev \
            postgresql-dev \
    && pyvenv /venv \
    && /venv/bin/pip install -U pip \
    && LIBRARY_PATH=/lib:/usr/lib /bin/sh -c "/venv/bin/pip install --no-cache-dir -r /requirements.txt" \
    && runDeps="$( \
            scanelf --needed --nobanner --recursive /venv \
                    | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
                    | sort -u \
                    | xargs -r apk info --installed \
                    | sort -u \
    )" \
    && apk add --virtual .python-rundeps $runDeps \
    && apk del .build-deps

# Se copia el contenido del directorio del Dockerfile al directorio "code" del container
RUN mkdir /code/
WORKDIR /code/
ADD . /code/

# uWSGI escuchara (esto solo indica que el container podria escuchar en este puerto, no lo abre propiamente tal, para ello hay que ejecutarlo con -p o -P, revisar documentacion)
EXPOSE 8000

# Agregar cualquier variable necesaria por Django o el archivo de configuracion:
ENV DJANGO_SETTINGS_MODULE=djangoProject.settings.deploy

# Configuracion uWSGI:
ENV UWSGI_VIRTUALENV=/venv UWSGI_WSGI_FILE=djangoProject/wsgi.py UWSGI_HTTP=:8000 UWSGI_MASTER=1 UWSGI_WORKERS=2 UWSGI_THREADS=8 UWSGI_UID=1000 UWSGI_GID=2000 UWSGI_LAZY_APPS=1 UWSGI_WSGI_ENV_BEHAVIOR=holy

# Variables de entorno pasadas al constuir la imagen
ARG SECRET
ARG POSTGRES_USER
ARG POSTGRES_PASSWORD
ENV SECRET=${SECRET} 
ENV POSTGRES_USER=${POSTGRES_USER}
ENV POSTGRES_PASSWORD=${POSTGRES_PASSWORD}

# Start uWSGI
CMD ["/venv/bin/uwsgi", "--http-auto-chunked", "--http-keepalive"]