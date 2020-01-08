FROM nginx:stable-alpine

# Update and install all of the required packages.
# At the end, remove the apk cache
RUN apk update && \
    apk upgrade && \
    apk add curl && \
    rm -rf /var/cache/apk/*

COPY index.html /usr/share/nginx/html

EXPOSE 80 443 	

CMD ["nginx", "-g", "daemon off;"]

HEALTHCHECK --interval=5m --timeout=3s --start-period=10s \
  CMD curl http://localhost/ || exit 1
