FROM alpine
MAINTAINER Roy Lines <https://roylines.co.uk>

RUN apk --no-cache add nginx
RUN mkdir -p /run/nginx
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
COPY nginx.conf /etc/nginx/nginx.conf

