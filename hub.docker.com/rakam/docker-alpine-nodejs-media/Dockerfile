FROM alpine:3.3

RUN apk update && apk add nodejs imagemagick ffmpeg wget unzip && rm -rf /var/cache/apk/*

ADD startup.sh /startup.sh
RUN chmod 755 /startup.sh

CMD ["ash", "/startup.sh"]
