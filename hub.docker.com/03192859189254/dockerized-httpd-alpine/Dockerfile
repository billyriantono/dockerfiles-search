#
# Do not change content here, image automatically built
#
FROM httpd:alpine

ARG BUILD_COMMIT
ARG BUILD_DATE

ENV \
	GENERAL_DOCKER_USERS_DEV="03192859189254" \
	GENERAL_DOCKER_USERS_PRD="alphasocket" \
	GENERAL_DOCKER_USER="alphasocket" \
	GENERAL_DOCKER_REGISTRIES_DEV="docker.io" \
	GENERAL_DOCKER_REGISTRIES_PRD="docker.io" \
	GENERAL_DOCKER_REGISTRY="docker.io" \
	GENERAL_KEYS_TRUE="True" \
	GENERAL_KEYS_FALSE="False" \
	GENERAL_KEYS_DEV="dev" \
	GENERAL_KEYS_PRD="prd" \
	BUILD_USER="03192859189254" \
	BUILD_REGISTRY="docker.io" \
	BUILD_REPO="https://github.com/alphaSocket/dockerized-httpd-alpine" \
	BUILD_BRANCH="latest" \
	BUILD_VERSION="latest" \
	BUILD_ENV="prd" \
	BUILD_HTTPD_PORT_DEV="80" \
	BUILD_HTTPD_PORT_PRD="443" \
	BUILD_FROM="httpd:alpine" \
	BUILD_NAME="httpd-alpine" \
	BUILD_PORTS_ADDITIONAL="" \
	BUILD_PORTS_MAIN="443" \
	BUILD_CMD="httpd-foreground" \
	SETUP_PATHS_BINARIES="/usr/local/bin" \
	SETUP_PATHS_SETUP="/usr/local/bin/setup" \
	SETUP_PATHS_CONFIG="/usr/local/bin/config" \
	SETUP_DEPENDENCIES_SETUP="" \
	SETUP_DEPENDENCIES_CONFIG="" \
	SETUP_DEPENDENCIES_RUNTIME="" \
	SETUP_HTTPD_CONF_PATH="/usr/local/apache2/conf" \
	SETUP_HTTPD_CONF_MAIN="/usr/local/apache2/conf/httpd.conf" \
	SETUP_HTTPD_CONF_CONFD="/usr/local/apache2/conf/conf.d" \
	SETUP_HTTPD_CONF_VHOSTD="/usr/local/apache2/conf/vhost.d" \
	SETUP_PHP_FPM="True" \
	CONFIG_REDINESS_TEST="true" \
	CONFIG_LIVENESS_TEST="true" \
	CONFIG_GROUPS_ADDITIONAL_ID="1001" \
	CONFIG_GROUPS_ADDITIONAL_NAME="" \
	CONFIG_GROUPS_MAIN_ID="1082" \
	CONFIG_GROUPS_MAIN_NAME="www-data" \
	CONFIG_USERS_ADDITIONAL_ID="1001" \
	CONFIG_USERS_ADDITIONAL_NAME="" \
	CONFIG_USERS_ADDITIONAL_GROUPS="" \
	CONFIG_USERS_MAIN_ID="1082" \
	CONFIG_USERS_MAIN_NAME="www-data" \
	CONFIG_USERS_MAIN_GROUPS="www-data" \
	CONFIG_HTTPD_SERVERNAME="httpd-alpine" \
	CONFIG_HTTPD_ALIAS="httpd-alpine" \
	CONFIG_HTTPD_TIMEOUT="1000" \
	CONFIG_HTTPD_DOCUMENT_ROOT="/var/www/html" \
	CONFIG_HTTPD_DOCUMENT_INDEX="index.php" \
	CONFIG_HTTPD_DOCUMENT_OPTIONS="FollowSymLinks" \
	CONFIG_PHP_PROXY_TIMEOUT="100" \
	CONFIG_PHP_PROXY_REGEX=".+\.ph(p[3457]?|t|tml)$" \
	CONFIG_PHP_FPM_HOST="php-fpm.service" \
	CONFIG_PHP_FPM_PORT="9000" \
	CONFIG_PATHS_CONTAINER_STATUS="/tmp/container_status" \
	CONFIG_PATHS_TEMPLATES_HTTPD_SERVER="/usr/local/templates/10-server.conf" \
	CONFIG_PATHS_TEMPLATES_HTTPD_SSL="/usr/local/templates/10-ssl.conf" \
	CONFIG_PATHS_TEMPLATES_HTTPD_FASTCGI="/usr/local/templates/20-fastcgi.conf" \
	CONFIG_PATHS_TEMPLATES_HTTPD_VHOST_DEV="/usr/local/templates/dev_vhost.conf" \
	CONFIG_PATHS_TEMPLATES_HTTPD_VHOST_PRD="/usr/local/templates/prd_vhost.conf" \
	CONFIG_PATHS_CONF_HTTPD_SERVER="/usr/local/apache2/conf/conf.d/10-server.conf" \
	CONFIG_PATHS_CONF_HTTPD_SSL="/usr/local/apache2/conf/conf.d/10-ssl.conf" \
	CONFIG_PATHS_CONF_HTTPD_FASTCGI="/usr/local/apache2/conf/conf.d/20-fastcgi.conf" \
	CONFIG_PATHS_CONF_HTTPD_VHOST="/usr/local/apache2/conf/vhost.d/main.conf"
ADD imports/bin/docker-config /usr/local/bin/docker-config
ADD imports/bin/docker-run /usr/local/bin/docker-run
ADD imports/bin/docker-rediness-test /usr/local/bin/docker-rediness-test
ADD imports/bin/docker-liveness-test /usr/local/bin/docker-liveness-test
ADD imports/bin/setup /usr/local/bin/setup/1519501355
ADD imports/bin/config /usr/local/bin/config/1519501355
ADD imports/templates/10-ssl.conf /usr/local/templates/10-ssl.conf
ADD imports/templates/20-fastcgi.conf /usr/local/templates/20-fastcgi.conf
ADD imports/templates/prd_vhost.conf /usr/local/templates/prd_vhost.conf
ADD imports/templates/10-server.conf /usr/local/templates/10-server.conf
ADD imports/templates/dev_vhost.conf /usr/local/templates/dev_vhost.conf


RUN chmod +x -R /usr/local/bin && \
    sync && \
    /usr/local/bin/setup/1519501355 1>/dev/stdout 2>/dev/stderr

EXPOSE 443 


ENTRYPOINT ["/bin/sh", "-c"]
CMD ["/usr/local/bin/docker-run"]

LABEL \
    org.label-schema.vcs-ref="$BUILD_COMMIT" \
    org.label-schema.vcs-url="https://github.com/alphaSocket/dockerized-httpd-alpine"