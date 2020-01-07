FROM mysql:5.7

# Set locale
RUN apt-get update && \
    apt-get install -y locales && \
    rm -rf /var/lib/apt/lists/* && \
    echo "ja_JP.UTF-8 UTF-8" > /etc/locale.gen && \
    locale-gen ja_JP.UTF-8
ENV LC_ALL ja_JP.UTF-8

# Generate settings
RUN { \
    echo "[mysqld]"; \
    echo 'character_set_server=utf8mb4'; \
    echo 'collation_server=utf8mb4_general_ci'; \
    echo 'init_connect="SET NAMES utf8mb4"'; \
    echo 'init_connect="SET collation_connection = utf8mb4_general_ci"'; \
    echo 'skip-character-set-client-handshake'; \
    echo '[mysql]'; \
    echo 'default_character_set=utf8mb4'; \
    echo '[client]'; \
    echo 'default_character_set=utf8mb4'; \
    } > /etc/mysql/conf.d/charset.cnf
