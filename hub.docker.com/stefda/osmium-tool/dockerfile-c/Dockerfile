FROM mariadb:10.3
RUN echo "[client] \n\
default-character-set=utf8mb4 \n\
[mysql] \n\
default-character-set=utf8mb4 \n\
[mysqld]\n\
collation-server = utf8mb4_unicode_ci \n\
init-connect='SET NAMES utf8mb4' \n\
character-set-server = utf8mb4" > /etc/mysql/conf.d/utf8.cnf
COPY rootfs /
RUN chown -R 999:999 /var/lib/mysql/
