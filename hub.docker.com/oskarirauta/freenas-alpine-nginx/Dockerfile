FROM oskarirauta/alpine-nginx:latest
LABEL org.freenas.interactive="false"                             \
      org.freenas.version="Latest (Auto Update)"			\
      org.freenas.upgradeable="true" 					\
      org.freenas.expose-ports-at-host="true" 				\
      org.freenas.privileged="false"                               \
      org.freenas.autostart="true" 					      \
      org.freenas.web-ui-protocol="http" 				      \
      org.freenas.web-ui-port="80" 					\
      org.freenas.web-ui-path="" 					      \
      org.freenas.port-mappings="80:80/tcp" \
      org.freenas.volumes="[						      \
          {							                  \
              \"name\": \"/config\",					\
              \"descr\": \"config storage space\"			\
          },                                                      \
          {							                  \
              \"name\": \"/webroot\",					      \
              \"descr\": \"public_html\"			      \
          }							                  \
      ]" 								            \
      org.freenas.settings="[ 					      \
          {							                  \
              \"env\": \"TZ\",					      \
              \"descr\": \"Timezone\",		      \
              \"optional\": true				            \
          },							            \
          {							                  \
              \"env\": \"PUID\",				            \
              \"descr\": \"UserID\",			            \
              \"optional\": true				            \
          },                                                      \
          {							                  \
              \"env\": \"PGID\",				            \
              \"descr\": \"GroupID\",		                  \
              \"optional\": true				            \
          } 							            \
      ]"
