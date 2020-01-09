FROM busybox:glibc

ENV NOMAD_VER=0.8.4

RUN wget https://releases.hashicorp.com/nomad/${NOMAD_VER}/nomad_${NOMAD_VER}_linux_amd64.zip \
    && unzip nomad_${NOMAD_VER}_linux_amd64.zip -d /usr/sbin/ \
    && rm nomad_${NOMAD_VER}_linux_amd64.zip

ENTRYPOINT [ "/usr/sbin/nomad" ]