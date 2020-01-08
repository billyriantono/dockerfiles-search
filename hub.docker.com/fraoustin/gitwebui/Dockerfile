FROM nginx:1.11
LABEL maintainer "fraoustin@gmail.com"

COPY ./docker/default.conf /etc/nginx/conf.d/default.conf

COPY ./docker/entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENV SET_CONTAINER_TIMEZONE false 
ENV CONTAINER_TIMEZONE "" 

RUN apt-get update && apt-get install -y \
        apache2-utils \
        fcgiwrap \
        git \
        git-core \
        python-pip \
        python-dev \
        libcgi-pm-perl \
        spawn-fcgi \
        uwsgi-plugin-python \
    && rm -rf /var/lib/apt/lists/* 

#manage user load fcgiwrap
RUN sed -i "s/www-data/nginx/g" /etc/init.d/fcgiwrap

RUN mkdir /usr/share/gitwebui
RUN mkdir /usr/share/gitwebui/docker-entrypoint.pre
RUN mkdir /usr/share/gitwebui/docker-entrypoint.post

# add cmd gitweb
COPY ./docker/cmd/addrepos.sh /usr/bin/addrepos
COPY ./docker/cmd/addauth.sh /usr/bin/addauth
COPY ./docker/cmd/rmrepos.sh /usr/bin/rmrepos
COPY ./docker/cmd/rmauth.sh /usr/bin/rmauth
RUN chmod +x /usr/bin/addrepos
RUN chmod +x /usr/bin/addauth
RUN chmod +x /usr/bin/rmrepos
RUN chmod +x /usr/bin/rmauth

ENV GITUSER gituser
ENV GITPASSWORD gitpassword

# add app gitwebui
RUN mkdir -p /var/www/app 
COPY ./docker/uwsgi.ini /var/www/app
RUN pip install uwsgi \
    && pip install gitwebui==0.1.1 \
    && mkdir -p /var/log/nginx/app /var/log/uwsgi/app \
    && chown -R www-data:www-data /var/www/app \
    && chown -R www-data:www-data /var/log
ENV GITWEBUI_REPO /var/lib/git/

VOLUME /var/lib/git
EXPOSE 80

# add for load
COPY ./docker/00_init.sh /usr/share/gitweb/docker-entrypoint.pre/00_init.sh
RUN chmod +x -R /usr/share/gitweb/docker-entrypoint.pre

ENTRYPOINT ["/entrypoint.sh"]
CMD ["app"]
