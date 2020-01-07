FROM lokaltog/baseimage:latest
MAINTAINER Kim Silkebækken <kim@dyktig.as>

EXPOSE 80 443

# Default git source, override in docker-compose.yml
ENV APP_ORIGIN git@bitbucket.org:User/repo.git
ENV APP_BRANCH master
ENV APP_COMMIT HEAD
ENV APP_ENV production
ENV APP_NAME fallback

# Redirect nginx logs to stdout/stderr
RUN mkdir -p /var/log/nginx
RUN ln -s /dev/stdout /var/log/nginx/access.log
RUN ln -s /dev/stderr /var/log/nginx/error.log

VOLUME /keys
VOLUME /var/www
VOLUME /var/www/node_modules

COPY conf/nginx.conf /etc/nginx/sites-enabled/default
COPY service/app /etc/service/app
