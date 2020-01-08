FROM alpine:edge
LABEL author="chillheart85@gmail.com"
LABEL version="2.0"
LABEL description="Alpine MongoDB 4.0 Docker Image"

RUN apk add --no-cache mongodb

VOLUME ["/data/db" ]
EXPOSE 27017

COPY run.sh /root
ENTRYPOINT [ "/root/run.sh" ]
CMD [ "mongod", "--bind_ip", "0.0.0.0" ]
