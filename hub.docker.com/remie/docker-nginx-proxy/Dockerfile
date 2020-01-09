
FROM nginx:latest

COPY ./proxy-template.conf /opt/nginx.conf

CMD [ "/bin/bash", "-c", "envsubst < /opt/nginx.conf > /etc/nginx/conf.d/default.conf && exec nginx -g 'daemon off;'" ]