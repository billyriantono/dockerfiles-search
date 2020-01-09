FROM nginx:1.13-alpine

LABEL maintainer="Whitepages Pro <prosupport@whitepages.com>"

ENV PORT 8080
ENV STATUS_ALLOWED_FROM 127.0.0.1
ENV ACCESS_LOG "/dev/stdout main"
ENV ERROR_LOG stderr
ENV RESOLVER 8.8.8.8

COPY docker-entrypoint.sh /
COPY *.template /etc/nginx/conf.d/

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["nginx", "-g", "daemon off;"]
