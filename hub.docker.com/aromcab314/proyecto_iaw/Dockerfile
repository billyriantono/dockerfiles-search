FROM iestriana/lamp
MAINTAINER Alejandro Roman Caballero


RUN apt-get update
ENV host=localhost
ENV contra_1=asdqwe123
ENV contra_2=890iopklñ
ENV gbd=alebuntu
ENV user_1=root
ENV user_2=condoriano

RUN echo "START"
ADD 000-default.conf /etc/apache2/sites-available/
ADD inicioservicio.sh /usr/bin/
RUN apt-get install -y git
WORKDIR /var/www/html/
RUN rm -rf index.html
RUN echo "<?php header('Location: ./PROYECTO_IAW_ROMAN_CABALLERO/index.php')?>" > index.php
#Clonacion del repositorio
RUN echo "Clonacion de repositorio";
RUN git clone https://github.com/Alejandro314/PROYECTO_IAW_ROMAN_CABALLERO.git
RUN chown -R www-data:www-data /var/www/html/PROYECTO_IAW_ROMAN_CABALLERO/
WORKDIR /var/www/html/PROYECTO_IAW_ROMAN_CABALLERO/PAGINA_WEB/ 
EXPOSE 80/udp
EXPOSE 80/tcp
EXPOSE 3306/tcp
RUN sh -c 'echo Europe/Madrid >/etc/timezone && dpkg-reconfigure -f noninteractive tzdata'
#Iniciar sevicios
RUN chmod 755 /usr/bin/inicioservicio.sh
ADD carga.sql /usr/bin
CMD /usr/bin/inicioservicio.sh


