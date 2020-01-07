FROM eclipse/php

USER root

# Update PHP to the latest version
RUN add-apt-repository ppa:ondrej/php -y && \
    apt-get update && \
    apt-get purge -y mysql-server* && \
    apt-get dist-upgrade -y && \
    apt-get autoremove -y

USER user
