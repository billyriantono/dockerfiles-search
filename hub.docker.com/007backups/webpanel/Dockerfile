FROM 007backups/base:3.2.1


ENV PYTHONUNBUFFERED 1
ENV DJANGO_SETTINGS_MODULE webpanel.settings

WORKDIR /usr/src/app

COPY requirements.txt /usr/src/app

RUN set -ex; \
	addgroup -g 82 -S www-data; \
	adduser -u 82 -D -S -G www-data www-data; \
    apk add --upgrade --no-cache --virtual .build-pkgs \
        build-base; \
#    apk add --upgrade --no-cache; \
    python3 -m pip install --no-cache-dir -r /usr/src/app/requirements.txt; \
    apk del .build-pkgs

COPY . /usr/src/app

RUN set -ex; \
    chown -R www-data:www-data /usr/src/app


EXPOSE 8001
CMD ["/usr/local/bin/uwsgi", \
    "--die-on-term", \
    "--http-socket", ":8001", \
    "--module", "webpanel.wsgi:application", \
    "--env", "DJANGO_SETTINGS_MODULE=webpanel.settings", \
    "--chdir", "/usr/src/app", \
    "--master", \
    "--binary-path", "/usr/local/bin/uwsgi", \
    "--no-orphans", \
    "--processes", "1", \
    "--uid", "www-data", \
    "--gid", "www-data", \
    "--harakiri", "20", \
    "--post-buffering", "1048576", \
    "--max-requests", "5000", \
    "--vacuum", \
    "--enable-threads", \
    "--thunder-lock"]
