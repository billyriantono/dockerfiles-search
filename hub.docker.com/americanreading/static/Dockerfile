FROM nginx:1.17

# Install authbind to allow listing on port 80 as a non-root user.
RUN apt-get update && \
  apt-get -y install \
    authbind && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Prepare files for a non-root user.
RUN mkdir /usr/local/src/app && \
  touch /var/run/nginx.pid && \
  touch /etc/authbind/byport/80 && \
  chown www-data:www-data /etc/authbind/byport/80 && \
  chmod 500 /etc/authbind/byport/80 && \
  chown -R www-data:www-data /var/run/nginx.pid && \
  chown -R www-data:www-data /var/cache/nginx && \
  chown -R www-data:www-data /etc/nginx && \
  chown -R www-data:www-data /usr/share/nginx/html

COPY ./nginx.conf /etc/nginx/nginx.conf
COPY ./site.conf /etc/nginx/conf.d/default.conf
COPY ./entrypoint /usr/local/bin/entrypoint

USER www-data

ENTRYPOINT ["entrypoint"]
