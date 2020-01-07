FROM httpd:2.4
LABEL org.freenas.interactive="false" \
      org.freenas.version="2" \
      org.freenas.upgradeable="true" \
      org.freenas.expose-ports-at-host="true" \
      org.freenas.autostart="true" \
      org.freenas.port-mappings="4280:80/tcp" \
      org.freenas.volumes="[ \
          { \
              \"name\": \"/usr/local/apache2/htdocs/\", \
              \"descr\": \"http web root directory\" \
          }   \
       ]" 
