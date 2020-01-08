FROM gitlab/gitlab-ce
LABEL org.freenas.interactive="false"			\
      org.freenas.version="1" 			\
      org.freenas.upgradeable="true" 			\
      org.freenas.expose-ports-at-host="true" 		\
      org.freenas.autostart="true" 			\
      org.freenas.bridged="true" 			\
      org.freenas.web-ui-protocol="http" 		\
      org.freenas.web-ui-port=""			\
      org.freenas.web-ui-path="" 			\
      org.freenas.port-mappings="443:443/tcp,80:80/tcp,22:22/tcp" 					\
      org.freenas.volumes="[				\
          {						\
              \"name\": \"/etc/gitlab\",			\
              \"descr\": \"config directory\"	\
          },						\
          {						\
              \"name\": \"/var/opt/gitlab\",			\
              \"descr\": \"data directrory\"		\
          }						\
          {						\
              \"name\": \"/var/log/gitlab\",			\
              \"descr\": \"log directory\"		\
          }						\
      ]"						\
      org.freenas.settings="[ 				\
      ]"
