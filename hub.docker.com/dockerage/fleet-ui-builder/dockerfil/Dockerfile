FROM dj4ngo/alpine-rpi

MAINTAINER sboyron <sebastien@boyron.eu>

RUN cross-build-start \
  apk -v update \
  apk -v upgrade \
  apk -v add --update nodejs nodejs-npm ca-certificates \
  cross-build-end

CMD ["sh"]

