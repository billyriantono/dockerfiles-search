FROM alpine:3.8
LABEL maintainer="Don Bowman <don@agilicus.com>"

ADD subst /usr/bin/subst
RUN apk add gettext

ENTRYPOINT ["/usr/bin/subst"]
