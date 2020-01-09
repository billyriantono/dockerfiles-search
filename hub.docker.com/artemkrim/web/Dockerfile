FROM nginx:1.17.1-alpine
RUN addgroup -S kitt && \
    adduser -u 1997 -S kitt -G kitt && \
    mkdir /opt/app/ && \
    touch /var/run/nginx.pid && \
    chown -R  kitt:kitt \
    /opt/app/ \
    /etc/nginx/ \
    /var/cache/nginx \
    /var/run/nginx.pid
USER kitt
COPY ./nginx.conf /etc/nginx/nginx.conf
COPY ./*.html /opt/app/
EXPOSE 8000
CMD ["nginx", "-g", "daemon off;"]
