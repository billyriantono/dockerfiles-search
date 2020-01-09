FROM nginx:1.15

WORKDIR /var/www

# Add Nginx configuration.
COPY security.conf /etc/nginx/
COPY performance.conf /etc/nginx/
COPY mime.types /etc/nginx/mime.types

# Add Symfony virtualhost template.
COPY symfony.template /etc/nginx/conf.d/symfony.template

# Add alternative CMD entrypoint that sets the Symfony virtualhost template.
COPY docker-nginx-entrypoint /usr/local/bin

CMD ["docker-nginx-entrypoint"]
