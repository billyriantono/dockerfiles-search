FROM tetraweb/php

RUN apt-get update 
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" 
RUN php composer-setup.php
RUN php -r "unlink('composer-setup.php');"
RUN which ssh-agent || ( apt-get update -y && apt-get install openssh-client -y )
RUN mkdir -p ~/.ssh