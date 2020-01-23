FROM alpine:3.8
MAINTAINER kost - https://github.com/kost

RUN apk --update add nginx-rtmp && rm -f /var/cache/apk/* && \
 mkdir -p /run/nginx && \
 echo "Success"

COPY root /

VOLUME ["/data"]

EXPOSE 1935 80

# ENTRYPOINT ["/scripts/run.sh"]
CMD ["nginx", "-g", "daemon off;"]

