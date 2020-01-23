ARG ALPINE_IMAGE=alpine

FROM "${ALPINE_IMAGE}"

RUN apk --no-cache add nsd

COPY /rootfs /

ENTRYPOINT [ "/entrypoint.sh" ]

CMD [ "nsd", "-d" ]
