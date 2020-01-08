FROM alpine:edge

RUN apk --no-cache add cmake make gcc g++ libc-dev cppcheck binutils-gold ninja
RUN apk --no-cache add ccache ca-certificates wget && update-ca-certificates
RUN apk --no-cache add freeglut-dev

ENV ENV=/etc/profile
COPY profile.sh /etc/profile.d/

CMD ["/bin/ash"]
