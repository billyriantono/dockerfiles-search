FROM hyperized/scratch as trigger

FROM alpine as builder

RUN apk -U add htop

FROM scratch

COPY --from=builder /usr/bin/htop /usr/bin/htop

