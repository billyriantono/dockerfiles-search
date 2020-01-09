FROM steamcache/steamcache-dns:latest
LABEL org.freenas.interactive="false" 		\
      org.freenas.version="02042017"		\
      org.freenas.upgradeable="true"		\
      org.freenas.expose-ports-at-host="true"	\
      org.freenas.autostart="true"		\
      org.freenas.capabilities-add="" \
      org.freenas.web-ui-protocol=""	\
      org.freenas.web-ui-port=\
      org.freenas.web-ui-path=""		\
      org.freenas.port-mappings="53:53/udp"			\
      org.freenas.volumes="[]"							\
      org.freenas.settings="[         \
          {             \
              \"env\": \"STEAMCACHE_IP\",        \
              \"descr\": \"IP address of steamcache server\",   \
              \"optional\": false    \
          } \
      ]"
