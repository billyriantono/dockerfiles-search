FROM danielguerra/alpine-sdk:edge as builder
MAINTAINER Daniel Guerra

RUN echo "sdk" | sudo  -S adduser -s /bin/false -D i2pd
WORKDIR /tmp/aports/testing/i2pd
RUN abuild-keygen -a -n
RUN abuild fetch
RUN abuild unpack
RUN abuild deps
RUN abuild prepare
RUN abuild build
RUN abuild rootpkg

FROM alpine:edge
MAINTAINER Daniel Guerra
COPY --from=builder /home/sdk/.abuild /tmp/.abuild
RUN find /tmp/.abuild -name "*.pub" -exec cp {} /etc/apk/keys \;
COPY --from=builder /home/sdk/packages/testing/x86_64/i2pd-2.18.0-r3.apk /tmp/i2pd-2.18.0-r3.apk
RUN apk --no-cache add /tmp/i2pd-2.18.0-r3.apk
RUN apk add --update --no-cache sudo boost
RUN mkdir -p /var/lib/i2pd/.i2pd
RUN ln -s /var/lib/i2pd/certificates /var/lib/i2pd/.i2pd/certificates
RUN chown  -R i2pd:i2pd /var/lib/i2pd
ADD bin /bin
USER i2pd
CMD ["cmd.sh"]
