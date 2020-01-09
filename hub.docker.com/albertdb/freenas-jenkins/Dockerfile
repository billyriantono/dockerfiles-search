FROM jenkins
LABEL org.freenas.interactive="false" 		\
      org.freenas.version="latest"		\
      org.freenas.upgradeable="false"		\
      org.freenas.expose-ports-at-host="true"	\
      org.freenas.autostart="true"		\
      org.freenas.web-ui-protocol="http"	\
      org.freenas.web-ui-port=8080		\
      org.freenas.port-mappings="8080:8080/tcp,50000:50000/tcp"	\
      org.freenas.volumes="[					\
          {							\
              \"name\": \"/var/jenkins_home\",			\
              \"descr\": \"Jenkins Database\"			\
          }							\
      ]"
