FROM alpine:edge

ENV depends="dynamips gns3-server qemu-img qemu-system-x86_64 ubridge vpcs"

RUN sed -n "s/main/testing/p" /etc/apk/repositories >> /etc/apk/repositories\
 && apk add --no-cache $depends

CMD ["gns3server"]

EXPOSE 3080
