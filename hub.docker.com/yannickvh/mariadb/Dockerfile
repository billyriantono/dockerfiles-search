FROM mariadb:10.2
MAINTAINER Yannick Vanhaeren

RUN set -ex \
    && sed -i -e "s|#default-character-set = utf8|default-character-set = utf8|" /etc/mysql/conf.d/mariadb.cnf \
    && sed -i -e "s|#character-set-server\s*= utf8|character-set-server = utf8|" /etc/mysql/conf.d/mariadb.cnf \
    && sed -i -e "s|#collation-server\s*= utf8_general_ci|collation-server = utf8_general_ci|" /etc/mysql/conf.d/mariadb.cnf \
    && sed -i -e "s|#character_set_server\s*= utf8|character_set_server = utf8|" /etc/mysql/conf.d/mariadb.cnf \
    && sed -i -e "s|#collation_server\s*= utf8_general_ci|collation_server = utf8_general_ci|" /etc/mysql/conf.d/mariadb.cnf \
    && sed -i -e "s|max_allowed_packet\s*= 16M|max_allowed_packet = 64M|" /etc/mysql/my.cnf
