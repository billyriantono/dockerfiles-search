FROM node:alpine as builder

RUN apk update && \
    apk add make git

COPY . /usr/src/app
WORKDIR /usr/src/app
RUN make install build

FROM nginx:alpine
COPY docker/nginx.conf /etc/nginx/nginx.conf
COPY --from=builder /usr/src/app/build /usr/share/nginx/html
EXPOSE 80
RUN chown nginx.nginx /usr/share/nginx/html/ -R
