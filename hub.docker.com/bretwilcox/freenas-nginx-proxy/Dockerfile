FROM jwilder/nginx-proxy:latest
LABEL org.freenas.interactive="false" \
      org.freenas.version="1.4" \
      org.freenas.upgradeable="false" \
      org.freenas.expose-ports-at-host="true" \
      org.freenas.autostart="true" \
      org.freenas.port-mappings="80:80/tcp,443:443/tcp" \
      org.freenas.volumes="[                                                          \
        {                                                                             \
            \"name\": \"/etc/nginx/certs\",                                           \
            \"descr\": \"Path to SSL certificates\",                                  \
            \"readonly\": \"true\"                                                    \
        },                                                                            \
        {                                                                             \
            \"name\": \"/etc/nginx/vhost.d\",                                         \
            \"descr\": \"Path to host configurations\",                               \
            \"readonly\": \"true\"                                                    \
        },                                                                            \
        {                                                                             \
            \"name\": \"/etc/nginx/htpasswd\",                                        \
            \"descr\": \"Path to htpasswd files named the same as the VIRTUAL_HOST\", \
            \"readonly\": \"true\"                                                    \
        }                                                                             \
      ]"                                                                              \
      org.freenas.static-volumes="[                                                   \
          {                                                                           \
              \"container_path\": \"/tmp/docker.sock\",                               \
              \"host_path\": \"/var/run/docker.sock\",                                \
              \"readonly\": \"true\"                                                  \
          }                                                                           \
      ]"                                                                              \
      org.freenas.settings="[                                                         \
            {                                                                         \
                \"env\": \"DEFAULT_HOST\",                                            \
                \"descr\": \"eg foo.bar.com\",                                        \
                \"optional\": true                                                    \
            }                                                                         \
      ]"

