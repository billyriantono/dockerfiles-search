FROM nginx:latest

COPY default.conf /etc/nginx/conf.d/default.conf
COPY wordpress.conf /etc/nginx/conf.d/wordpress.conf
COPY restrictions.conf /etc/nginx/conf.d/restrictions.conf
COPY proxy.conf /etc/nginx/conf.d/proxy.conf
COPY docker-entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
CMD ["nginx", "-g", "daemon off;"]