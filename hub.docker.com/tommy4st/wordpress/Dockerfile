FROM wordpress

RUN apt-get update && apt-get install -y libldap2-dev \
 && docker-php-ext-install -j$(nproc) ldap \
 && a2enmod authnz_ldap \
 && rm -rf /var/lib/apt/lists/*
