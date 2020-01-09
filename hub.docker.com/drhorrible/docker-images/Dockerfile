FROM ampache/ampache:latest			
LABEL org.freenas.interactive="false" 					\
      org.freenas.version="1" 					\
      org.freenas.upgradeable="false" 					\
      org.freenas.expose-ports-at-host="true" 				\
      org.freenas.autostart="true" 					\
      org.freenas.web-ui-protocol="http" 				\
      org.freenas.web-ui-port="80" 					\
      org.freenas.web-ui-path="" 					\
      org.freenas.port-mappings="8080:80/tcp" 		\
      org.freenas.volumes="[						\
          {							\
              \"name\": \"/var/www/config\",					\
              \"descr\": \"Config storage space\"				\
          },							\
          {							\
              \"name\": \"/var/www/themes\",					\
              \"descr\": \"Themes storage space\"				\
          },							\
          {							\
              \"name\": \"/media\",					\
              \"descr\": \"media volume\"				\
          }							\
      ]" 								\
      org.freenas.settings="[ 					\
          {							\
              \"env\": \"PGID\",					\
              \"descr\": \"GroupID\",					\
              \"optional\": true					\
          },							\
          {							\
              \"env\": \"PUID\",					\
              \"descr\": \"UserID\",					\
              \"optional\": true					\
         }							\
      ]"								\
      org.freenas.static-volumes="[					\
          {							\
              \"container_path\": \"/etc/localtime\",			\
              \"host_path\": \"/etc/localtime\",				\
              \"readonly\": \"true\"					\
          }							\
      ]"
