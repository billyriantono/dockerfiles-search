FROM alpine:3.11.3 AS BUILD-ENV
LABEL maintainer "Anucha Nualsi <ana.cpe9@gmail.com>"

ADD qemu-aarch64-static /usr/bin
RUN chmod +x /usr/bin/qemu-aarch64-static

FROM arm64v8/alpine:3.11.3
LABEL maintainer="Anucha Nualsi <ana.cpe9@gmail.com>"

COPY --from=BUILD-ENV /usr/bin/qemu-aarch64-static /usr/bin
