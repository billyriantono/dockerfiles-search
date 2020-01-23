FROM alpine:3.8
LABEL maintainer="Marc Wickenden <marc@4armed.com>"

RUN apk add --update perl-crypt-ssleay \
                     perl-lwp-useragent-determined

WORKDIR /app

COPY padBuster.pl .
RUN chmod +x padBuster.pl

ENTRYPOINT [ "./padBuster.pl" ]

