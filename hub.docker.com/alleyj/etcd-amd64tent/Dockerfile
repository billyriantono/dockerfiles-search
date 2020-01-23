FROM pducharme/unifi-video-controller
LABEL org.freenas.interactive="false"                           \
      org.freenas.version="1"                                   \
      org.freenas.upgradeable="false"                           \
      org.freenas.expose-ports-at-host="true"                   \
      org.freenas.autostart="true"                              \
      org.freenas.capabilities-add="SYS_ADMIN,DAC_READ_SEARCH"  \
      org.freenas.web-ui-protocol="http"                        \
      org.freenas.web-ui-port=7080                              \
      org.freenas.port-mappings="7443:7443/tcp,7445:7445/tcp,7446:7446/tcp,7447:7447/tcp,7080:7080/tcp,6666:6666/tcp"                 \
      org.freenas.volumes="[                         \
          {                                          \
              \"name\": \"/var/lib/unifi-video\",            \
              \"descr\": \"data dir\" \
          },                                          \
	  {                                           \
	      \"name\": \"/usr/lib/unifi-video/data/videos\",     \
	      \"descr\": \"videos dir\" \
	  },                                          \
	  {                                           \
	      \"name\": \"/var/log/unifi-video\",                 \
	      \"descr\": \"logs dir\"   \
	  }                                           \
      ]"                                             \
      org.freenas.settings="[                                                            \
          {                                                                              \
              \"env\": \"TZ\",                                                     \
              \"descr\": \"TimeZone\",                               \
              \"optional\": true                                                        \
          },                                                                             \
          {                                                                              \
              \"env\": \"PUID\",                                                  \
              \"descr\": \"puid\", \
              \"optional\": true                                                         \
          },                                                                             \
          {                                                                              \
              \"env\": \"PGID\",                                                         \
              \"descr\": \"pgid\",                     \
              \"optional\": true                                                         \
          },                                                                             \
          {                                                                              \
              \"env\": \"DEBUUG\",                                                         \
              \"descr\": \"Debug\",                   \
              \"optional\": true                                                         \
          }                                                                             \
      ]"
