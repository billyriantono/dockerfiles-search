FROM alpine:3.9 AS builder
RUN apk add --no-cache make
COPY . /tugboat
RUN make -C /tugboat install

FROM docker/compose:1.24.1
RUN apk add --no-cache bash git openssh-client vim dockerpy-creds
COPY docker-entrypoint.sh /usr/local/sbin/
COPY --from=builder /usr/ /usr/
ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["/bin/bash"]
