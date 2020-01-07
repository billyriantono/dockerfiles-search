FROM java:7-jre-alpine

WORKDIR /services/sqs

RUN apk update && \
    apk add axel && \
    axel -a -n 5 https://s3-eu-west-1.amazonaws.com/softwaremill-public/elasticmq-server-0.9.3.jar && \
    mv elasticmq-server-0.9.3.jar server.jar

COPY config/elasticmq.conf elasticmq.conf

COPY run.sh /

CMD ["/run.sh"]
