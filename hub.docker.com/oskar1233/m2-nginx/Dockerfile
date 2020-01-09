FROM nginx:alpine

VOLUME /var/www
VOLUME /etc/nginx
VOLUME /var/log/nginx/log

# You can override these in command line, docker-compose, k8s config or wherever
ARG FPM_SERVER=fpm:9000
ARG DOMAIN=example.com
ARG PORT=80

ENV FPM_SERVER=${FPM_SERVER}
ENV DOMAIN=${DOMAIN}
ENV PORT=${PORT}

COPY config /nginx-config
COPY nginx-envsubst.sh .
COPY entrypoint.sh .

CMD ["./entrypoint.sh"]
