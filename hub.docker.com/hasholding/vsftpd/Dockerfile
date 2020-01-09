FROM hasholding/alpine-base

LABEL maintainer "Levent SAGIROGLU <LSagiroglu@gmail.com>"

RUN \
apk update && apk upgrade &&  apk --update add --no-cache  vsftpd openssl \
&& apk --update add --no-cache --virtual .build-dependencies build-base linux-pam-dev curl tar   

VOLUME /shared

COPY etc /etc/vsftpd
COPY entrypoint.sh /bin/
COPY README.md /shared/README.md

ENV VSFTPD_CFG=/etc/vsftpd/vsftpd.conf
ENV VSFTPD_PWDFLE=/etc/vsftpd/virtual_users


RUN \
  mkdir /pam && \
  cd pam && \
  curl -sSL https://github.com/prapdm/libpam-pwdfile/archive/v1.0.tar.gz | tar xz --strip 1 && \
  make install && \
  cd .. && \
  rm -rvf pam && \
  mkdir -p /var/run/vsftpd/empty && \
  apk del .build-dependencies && \
  rm -rvf /var/cache/apk/* && \
  rm -rvf /tmp/* && \
  rm -rvf /src  && \
  rm -rvf /var/log/* 
 

EXPOSE 21 21100-21110

CMD  /bin/entrypoint.sh
