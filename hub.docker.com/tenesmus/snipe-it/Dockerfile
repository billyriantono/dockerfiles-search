FROM snipe/snipe-it
LABEL maintainer Nathan Douglas <ndouglas@ainonline.com>
RUN sed -i 's/post_max_size = .*/post_max_size = 128M/' /etc/php/7.0/apache2/php.ini
RUN sed -i 's/upload_max_filesize = .*/upload_max_filesize = 128M/' /etc/php/7.0/apache2/php.ini
RUN sed -i 's/post_max_size = .*/post_max_size = 128M/' /etc/php/7.0/cli/php.ini
RUN sed -i 's/upload_max_filesize = .*/upload_max_filesize = 128M/' /etc/php/7.0/cli/php.ini
