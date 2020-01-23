FROM redmine:latest
LABEL org.freenas.interactive="false"			\
      org.freenas.version="1"				\
      org.freenas.upgradeable="true"			\
      org.freenas.expose-ports-at-host="true"		\
      org.freenas.autostart="true"			\
      org.freenas.web-ui-protocol="http" \
      org.freenas.web-ui-port=8080 \
      org.freenas.web-ui-path="" \
      org.freenas.port-mappings="8080:8080/tcp"	\
      org.freenas.volumes="[				\
          {						\
              \"name\": \"/usr/src/redmine/files\",	\
              \"descr\": \"Data directory\"	\
          }						\
       ]"						\
       org.freenas.settings="[				\
          {						\
              \"env\": \"REDMINE_NO_DB_MIGRATE\",	\
              \"descr\": \"This variable allows you to control if rake db:migrate is run on container start\",		\
              \"optional\": true			\
          },						\
          {						\
              \"env\": \"REDMINE_SECRET_KEY_BASE\",	\
              \"descr\": \"This variable is used to create an initial config/secrets.yml and set the secret_key_base value, which is used by Rails to encode cookies storing session data thus preventing their tampering.\",		\
              \"optional\": true			\
          }						\
      ]"                                                           
