FROM alpine

EXPOSE 8118 9050

RUN apk --no-cache add privoxy tor s6 su-exec

COPY service /etc/service/

CMD ["s6-svscan", "/etc/service"]
