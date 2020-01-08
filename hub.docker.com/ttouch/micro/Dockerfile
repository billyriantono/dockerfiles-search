FROM alpine:3.2
RUN apk add --update ca-certificates tzdata && \
    rm -rf /var/cache/apk/* /tmp/*
ADD micro /micro
RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
ENV MICRO_REGISTRY kubernetes
ENV MICRO_API_NAMESPACE retail.api
ENV MICRO_API_HANDLER rpc
WORKDIR /
EXPOSE 8080
ENTRYPOINT [ "/micro" ]
