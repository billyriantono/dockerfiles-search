FROM golang:1.10 as loaderapp

COPY cmd/nginx_loader /nginx_loader
WORKDIR /nginx_loader
RUN go build

FROM nginx:1.15.0
WORKDIR /
COPY modules/hostname_service/nginx.conf.tpl .
COPY --from=loaderapp /nginx_loader/nginx_loader .

CMD ["./nginx_loader", "/nginx.conf.tpl"]
