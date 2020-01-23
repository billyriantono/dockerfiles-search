# This dockerfile builds a php 7.3/nginx image with SQL Server drivers.
FROM webdevops/php-nginx-dev:7.3
MAINTAINER Mark Thornburgh "mthornburgh@edgehomes.com"

#Install custom service configuration
COPY assets/php.development.ini /opt/docker/etc/php/php.ini
COPY assets/10-general.conf /opt/docker/etc/nginx/vhost.common.d/10-general.conf
COPY assets/dev-entrypoint.sh /dev-entrypoint.sh
COPY assets/wkhtmltox_0.12.5-1.stretch_amd64.deb /wkhtmltox_0.12.5-1.stretch_amd64.deb

#Install dependencies
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list && \
    curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
    ACCEPT_EULA=Y apt-get install -y msodbcsql17 unixodbc-dev mssql-tools nodejs iputils-ping iproute2 && \
    echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> /root/.bash_profile && \
    echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> /root/.bashrc && \
    pecl install sqlsrv pdo_sqlsrv && \
    apt install -y /wkhtmltox_0.12.5-1.stretch_amd64.deb && \
    rm -rf /var/lib/apt/lists/* && \
    rm /wkhtmltox_0.12.5-1.stretch_amd64.deb && \
    npm i -g npm gulp-cli gulp sass && \
    chmod 0755 /dev-entrypoint.sh

CMD /dev-entrypoint.sh
