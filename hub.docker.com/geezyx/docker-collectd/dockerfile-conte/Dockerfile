FROM codercom/code-server:2.1698

USER root

RUN wget -O /go.deb https://deb.geek1011.net/pool/main/g/go/go_1.13-godeb1_amd64.deb && dpkg -i /go.deb && rm /go.deb
RUN apt install -y libc6-dev busybox-static rsync gnupg2 man-db git build-essential python3 ncdu htop jq curl nano autoconf automake

COPY init.sh /init.sh
ENTRYPOINT ["dumb-init", "/bin/sh", "/init.sh"]
