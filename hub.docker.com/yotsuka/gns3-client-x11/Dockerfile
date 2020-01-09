FROM alpine:edge

ENV depends="\
    gns3-gui\
    ttf-ubuntu-font-family\
    wireshark\
    xkeyboard-config\
    xterm\
"

RUN sed -n "s/main/testing/p" /etc/apk/repositories >> /etc/apk/repositories\
 && apk add --no-cache $depends

CMD ["gns3"]
