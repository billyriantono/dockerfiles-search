FROM nginx:alpine
RUN apk add --no-cache bash
COPY nginx.template /etc/nginx/nginx.template

CMD ["/bin/bash", "-c", "envsubst '$${LARAVEL_HOST},$${LARAVEL_PORT},$${ECHO_SERVER_HOST},$${ECHO_SERVER_PORT}' < /etc/nginx/nginx.template > /etc/nginx/nginx.conf && exec nginx -g 'daemon off;'"]