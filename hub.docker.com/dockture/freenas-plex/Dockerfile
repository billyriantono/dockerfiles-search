FROM linuxserver/plex:latest
LABEL org.freenas.interactive="false" \
      org.freenas.version=1 \
      org.freenas.upgradeable="true" \
      org.freenas.expose-ports-at-host="true" \
      org.freenas.autostart="true" \
      org.freenas.web-ui-protocol="http" \
      org.freenas.web-ui-port=32400 \
      org.freenas.web-ui-path="" \
      org.freenas.port-mappings="1900:1900/udp,32469:32469/udp,32400:32400/tcp,32400:32400/udp,32469:32469/tcp,5353:5353/udp" \
      org.freenas.volumes="[						\
          {								\
              \"name\": \"/config\",					\
              \"descr\": \"Plex config files\"			\
          },								\
          {								\
              \"name\": \"/data\",			\
              \"descr\": \"Plex library \"		\
          }								\
      ]" \
     org.freenas.settings="[ 						                        \
          {								                                    \
              \"env\": \"TZ\",					                              \
              \"descr\": \"Timezone information, eg Europe/London\",				\
              \"optional\": true					                              \
          },								                              \
          {								                                    \
              \"env\": \"PUID\",					                              \
              \"descr\": \"User ID \",				\
              \"optional\": true					                              \
          },								                              \
          {								                                    \
              \"env\": \"PGID\",					                        \
              \"descr\": \"Group ID\",				\
              \"optional\": true					                              \
          }	                                                                              \
      ]"
