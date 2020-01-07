FROM jwilder/nginx-proxy:latest
MAINTAINER Philipp Goellner <philipp.goellner@xaltbc.de>

ENV NGINX_HOME                      /etc/nginx
ENV NGINX_HOME_DEFAULTS             /etc/nginx_defaults

ENV TIME_ZONE                       false

ENV BACKUP_HOST                     false
ENV BACKUP_PATH                     false
# If you do not want to restore certs, conf.d, html or vhost.d, set the BACKUP_PATH_* to "false"
ENV BACKUP_PATH_CERTS               certs
ENV BACKUP_PATH_CONF                conf.d
ENV BACKUP_PATH_HTML                html
ENV BACKUP_PATH_VHOST               vhost.d
#
ENV BACKUP_USER                     false
ENV BACKUP_KEY_FILE                 /tmp/id_rsa

# Copy my_proxy.conf file
RUN mkdir -p                        ${NGINX_HOME_DEFAULTS}/conf.d/
COPY my_proxy.conf                  ${NGINX_HOME_DEFAULTS}/conf.d/
COPY configure-and-start-root.sh    /
RUN chmod u+x                       /configure-and-start-root.sh \
 && apt-get update --quiet \
 && apt-get install --quiet -y --no-install-recommends openssh-client \
                                                       rsync \
 && apt-get clean

VOLUME ["/tmp/docker.sock"]
VOLUME ["${NGINX_HOME}/certs"]
VOLUME ["${NGINX_HOME}/conf.d"]
VOLUME ["/usr/share/nginx/html"]
VOLUME ["${NGINX_HOME}/vhost.d"]

ENTRYPOINT ["/configure-and-start-root.sh"]
CMD ["forego start -r"]
