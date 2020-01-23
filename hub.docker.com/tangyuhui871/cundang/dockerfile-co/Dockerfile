FROM alpine:3.8

COPY env.sh /

RUN apk update && apk upgrade && \
    apk add nginx && \
    chmod +x env.sh

COPY nginx.conf /etc/nginx/nginx.conf

COPY nginx.vh.default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80 

ENTRYPOINT ["sh", "/env.sh"]
CMD ["nginx", "-c", "/etc/nginx/nginx.conf" "-g", "daemon off;"]
