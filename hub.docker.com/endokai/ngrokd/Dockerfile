FROM ubuntu:14.04
MAINTAINER endokai
ENV USER root
ENV HTTP_PORT 80
ENV HTTPS_PORT 443
ENV TUNNEL_PORT 4443
ENV NGROK_DONAMIN ngrok.io
ADD ngrokd_linux /tmp/ngrokd
ADD run.sh /tmp/run.sh
ADD server.crt /tmp/server.crt
ADD server.key /tmp/server.key
EXPOSE 80 443 4443

RUN set -ex \
  && cd /tmp \
  && install -v -D ngrokd /bin/ngrokd \
  && install -v -D run.sh /bin/run.sh \
  && install -v -D server.crt /bin/server.crt \
  && install -v -D server.key /bin/server.key
ENTRYPOINT ["run.sh"]
