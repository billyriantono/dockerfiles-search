FROM nginx
MAINTAINER Bram van Dartel <root@rootrulez.com>

RUN mkdir -p /munki_repo && \
    mkdir -p /etc/nginx/sites-enabled/

COPY ./app /app

RUN cp /app/nginx.conf /etc/nginx/nginx.conf && \
    cp /app/munki-repo.conf /etc/nginx/sites-enabled/

VOLUME /munki_repo

EXPOSE 80
