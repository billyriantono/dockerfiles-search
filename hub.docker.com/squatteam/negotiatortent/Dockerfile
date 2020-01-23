FROM wordpress:php7.2

# Setup prerequisites.
RUN apt-get update && apt-get install -my apt-transport-https wget gnupg

# Install Microsoft ODBC.
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
	&& curl https://packages.microsoft.com/config/debian/9/prod.list | tee --append /etc/apt/sources.list.d/mssql-release.list \
	&& apt-get update \
	&& ACCEPT_EULA=Y apt-get install msodbcsql17 -y

# Install Microsoft SQL Driver for Linux.
RUN apt-get install unixodbc unixodbc-dev -y \
	&& pecl install sqlsrv-5.6.1 \ 
	&& pecl install pdo_sqlsrv-5.6.1 \
	&& docker-php-ext-enable sqlsrv pdo_sqlsrv
