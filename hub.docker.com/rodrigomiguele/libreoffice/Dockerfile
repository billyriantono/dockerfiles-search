FROM alpine

RUN apk add --update libreoffice && \
    apk info --purge

RUN addgroup developer && adduser developer -G developer -h /home/developer -D
USER developer
WORKDIR /home/developer/

ENTRYPOINT ["libreoffice"]
