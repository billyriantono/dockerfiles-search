FROM alpine:3.11.2
LABEL maintainer="Shawn Friedel <emailshawnf@gmail.com>"
RUN apk add --no-cache curl bash &&\
curl -sSL https://git.io/get-mo -o mo &&\
chmod +x mo &&\
mv mo /usr/local/bin/
ENTRYPOINT [ "/bin/sh" ]
