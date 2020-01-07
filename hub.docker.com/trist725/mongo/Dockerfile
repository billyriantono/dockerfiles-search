FROM alpine
RUN apk add --no-cache mongodb
VOLUME ["/db/data", "/db/log"]
EXPOSE 27017 2379
CMD mongod --bind_ip_all --ipv6 --dbpath /db/data --logpath /db/log/mongod.log --directoryperdb
