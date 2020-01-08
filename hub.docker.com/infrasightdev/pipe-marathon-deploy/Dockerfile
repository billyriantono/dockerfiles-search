FROM alpine:3.8

RUN apk update && apk add bash gettext curl

COPY pipe /
RUN chmod a+x /*.sh

ENTRYPOINT ["/pipe.sh"]
