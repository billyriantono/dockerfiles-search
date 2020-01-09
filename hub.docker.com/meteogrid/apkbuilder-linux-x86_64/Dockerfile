FROM meteogrid/base-linux-x86_64:latest

ENV PACKAGES="\
alpine-sdk \
coreutils \
python2@edge \
python2-dev@edge \
"

RUN apk --update --no-cache upgrade \
  && apk  --no-cache add $PACKAGES \
  && adduser -G abuild -g "Meteogrid Alpine Package Builder" -s /bin/ash -D meteogrid \
  && echo "meteogrid ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers \
  && mkdir -p /packages /etc/apk/cache /var/cache/distfiles \
  && chown meteogrid:abuild /packages /etc/apk/cache /var/cache/distfiles
COPY abuilder /bin/
RUN sed -i 's/-Os -fomit-frame-pointer/-O2 -fomit-frame-pointer/g'  /etc/abuild.conf
USER meteogrid
WORKDIR /home/meteogrid/meteogrid
ENV RSA_PRIVATE_KEY_NAME ssh.rsa
ENV PACKAGER_PRIVKEY /home/meteogrid/${RSA_PRIVATE_KEY_NAME}
ENV REPODEST /packages
ENTRYPOINT ["abuilder"]
