FROM goofball222/unifi:latest

ARG BUILD_DATE
ARG VERSION=5.9.29

LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-url="https://github.com/sisaenkov/freenas10/tree/master/unifi" \
      org.label-schema.version=$VERSION \
      org.label-schema.schema-version="1.0"

LABEL description="UniFi Controller"
LABEL org.freenas.interactive="false" \
      org.freenas.version=$VERSION \
      org.freenas.upgradeable="false" \
      org.freenas.expose-ports-at-host="true" \
      org.freenas.autostart="true" \
      org.freenas.web-ui-protocol="https" \
      org.freenas.web-ui-port="8443" \
      org.freenas.web-ui-path="manage" \
      org.freenas.port-mappings="3478:3478/udp,6789:6789/tcp,8080:8080/tcp,8443:8443/tcp,8843:8843/tcp,8880:8880/tcp,10001:10001/udp" \
      org.freenas.volumes="[						\
          {								\
              \"name\": \"/usr/lib/unifi/data\",			\
              \"descr\": \"UniFi Configuration Data\"			\
          },								\
          {								\
              \"name\": \"/usr/lib/unifi/cert\",			\
              \"descr\": \"UniFi Controller Certificates\"		\
          }								\
      ]"								\
      org.freenas.settings="[						\
          {								\
              \"env\": \"TZ\",						\
              \"descr\": \"Timezone - eg Europe/Moscow\",		\
              \"optional\": true					\
          }								\
      ]"
