FROM babim/alpinebase

RUN apk --no-cache add tinyproxy
ENTRYPOINT ["/usr/sbin/tinyproxy"]
EXPOSE 8888
CMD ["-d"]
