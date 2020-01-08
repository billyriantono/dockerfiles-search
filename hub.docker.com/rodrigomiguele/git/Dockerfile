FROM alpine

RUN apk add --update git openssh-client && \
    apk info --purge

RUN addgroup developer && adduser developer -G developer -h /home/developer -D
USER developer
WORKDIR /home/developer/workspace

ENTRYPOINT ["git"]

CMD ["--version"]
