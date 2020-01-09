FROM nginx:1.15.8-alpine

# Install htpasswd tool.
RUN apk add --update apache2-utils && rm -rf /var/cache/apk/*

# Add nginx config.
COPY ./nginx.conf /etc/nginx/nginx.conf

# Set timezone for nginx.
ENV TZ "Europe/Amsterdam"

# Install dumb init.
RUN apk add --update dumb-init && rm -rf /var/cache/apk/*

# Add entrypoint script.
COPY ./entrypoint.sh /tmp/entrypoint.sh
RUN chmod 755 /tmp/entrypoint.sh
CMD ["/tmp/entrypoint.sh"]

EXPOSE 80
