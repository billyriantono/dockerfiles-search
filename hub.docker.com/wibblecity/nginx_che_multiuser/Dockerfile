FROM nginx:1.14.1-alpine

### required input
ARG IDE_ORIGIN

### environment variables
ENV NGINX_CFG_FILE_DIR="/etc/nginx/conf.d"
ENV NGINX_CFG_FILE_NAME="default.conf"
ENV NGINX_CFG_FILE_PATH="${NGINX_CFG_FILE_DIR}/${NGINX_CFG_FILE_NAME}"

### copying config files
COPY "${NGINX_CFG_FILE_NAME}" "${NGINX_CFG_FILE_DIR}"
COPY entrypoint.sh /usr/bin/entrypoint.sh

### setting permissions
RUN chmod 700 /usr/bin/entrypoint.sh

### entrypoint
ENTRYPOINT ["/usr/bin/entrypoint.sh"]
