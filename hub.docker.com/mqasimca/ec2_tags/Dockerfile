FROM alpine:latest

COPY EC2-Tags.sh /bin/
RUN apk -v --update add groff less python py-pip wget \
    && pip install awscli \ 
    && apk --purge -v del py-pip \
    && chmod 777 /bin/EC2-Tags.sh \
    && rm /var/cache/apk/*

ENTRYPOINT ["EC2-Tags.sh"]
