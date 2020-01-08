FROM alpine as builder

RUN apk update && \
    apk add gcc libc-dev

COPY a.c /

RUN gcc -o /a a.c

FROM alpine

COPY --from=builder /a /a

CMD ["/a"]
