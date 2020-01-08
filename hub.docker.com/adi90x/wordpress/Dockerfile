FROM wordpress
RUN apt update && apt install -y libmcrypt-dev sendmail sendmail-bin mailutils && docker-php-ext-install mcrypt sockets && rm -rf /var/lib/apt/lists/*
