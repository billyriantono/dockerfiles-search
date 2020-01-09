FROM alpine

RUN apk --update add python py-pip bash && \
    pip install s4cmd && \
    rm -fr /var/cache/apk/*

ENTRYPOINT ["s4cmd"]
CMD ["ls"]