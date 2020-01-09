FROM frolvlad/alpine-fpc:slim AS builder-image

COPY one_second.pas /
RUN fpc -Mfpc -O2 /one_second.pas


FROM alpine:3.9

COPY --from=builder-image /one_second /

CMD ["/usr/bin/time", "-f", "%U", "/one_second"]
