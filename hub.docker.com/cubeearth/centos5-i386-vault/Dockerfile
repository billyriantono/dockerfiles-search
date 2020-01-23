FROM alpine AS unpacked
RUN apk --no-cache add wget tar && \
	mkdir -p /tmp/unpacked && \
	wget --no-check-certificate -qO- /tmp https://github.com/Cube-Earth/container-centos5-i386-vault-build/releases/download/1.0/centos5.tar.gz | tar -C /tmp/unpacked -xz

FROM scratch
COPY --from=unpacked /tmp/unpacked /
ENTRYPOINT ["linux32"]
