FROM patricol/ubuntu:gpu as ubuntu

#https://github.com/neutrinolabs/xrdp/releases
#https://github.com/neutrinolabs/xorgxrdp/releases

ENV XRDP_VERSION=0.9.9 XORGXRDP_VERSION=0.2.9 SAVEDIR=/tmp/files_to_save
COPY ./*-xrdp.sh /tmp/
RUN chmod +x /tmp/*-xrdp.sh \
 && sync \
 && /tmp/compile-xrdp.sh

FROM scratch
COPY --from=ubuntu /tmp/files_to_save/ /
