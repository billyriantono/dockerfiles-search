FROM alpine

COPY files /
RUN apk add git bash curl

ENTRYPOINT ["/bin/bash", "/check_for_update.sh" ]
