FROM alpine:3.9 as mongo
RUN apk --update --no-cache add mongodb && mkdir -p /data/db
CMD ["mongod", "--bind_ip_all"]
