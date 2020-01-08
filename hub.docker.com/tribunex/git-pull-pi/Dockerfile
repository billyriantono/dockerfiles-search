FROM multiarch/alpine:armhf-v3.9 

RUN apk --update --no-cache add git && \
    rm -rf /tmp/* /var/tmp/* /var/cache/apk/*

COPY run.sh .
RUN chmod +x run.sh

CMD ["sh","run.sh"]