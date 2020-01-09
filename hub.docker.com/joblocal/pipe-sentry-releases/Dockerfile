FROM alpine:3.8

LABEL maintainer="joblocal GmbH <produktentwicklung@joblocal.de>"

RUN apk update && apk add bash curl

COPY pipe /
RUN chmod a+x /*.sh

ENTRYPOINT ["/pipe.sh"]
