FROM nginx:alpine
LABEL maintainer="ccmite"
WORKDIR /

RUN apk --update upgrade && \
    apk add --no-cache --no-progress \
    nginx-mod-stream && \
    mkdir -p /var/run/nginx

COPY nginx.conf /etc/nginx/nginx.conf

ENTRYPOINT ["/usr/sbin/nginx", "-g", "daemon off;"]
EXPOSE 25565
