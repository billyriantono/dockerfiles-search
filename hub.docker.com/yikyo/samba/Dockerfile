FROM alpine:3.4

MAINTAINER yikyo <yikyo666@gmail.com>

RUN sed -i -e 's/dl-cdn\.alpinelinux\.org/mirrors\.ustc\.edu\.cn/g' /etc/apk/repositories

RUN apk add --update --no-cache samba

ADD smb.conf /etc/samba

EXPOSE 139 445

VOLUME ["/home/workspace"]

ENTRYPOINT ["smbd", "-FS"]
