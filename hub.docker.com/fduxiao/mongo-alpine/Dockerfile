FROM alpine
RUN apk --update --no-cache add mongodb
VOLUME ["/data/db"]
EXPOSE 27017
CMD ["mongod"]
