FROM alpine
EXPOSE 80
STOPSIGNAL SIGTERM
CMD ["nginx", "-g", "daemon off;"]
RUN apk add --no-cache nginx && \
mkdir -p /run/nginx
COPY default.conf /etc/nginx/conf.d/default.conf
COPY index.html /var/lib/nginx/html/index.html
