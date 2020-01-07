FROM nginx:1.15.12

RUN apt-get update && apt-get install -y --no-install-recommends libcap2-bin

RUN setcap 'cap_net_bind_service=+ep' /usr/sbin/nginx

RUN touch /var/run/nginx.pid && \
  chown -R www-data:www-data /var/run/nginx.pid && \
  chown -R www-data:www-data /var/cache/nginx

USER www-data
