FROM debian:stretch-slim                                                                                                                                                                      
RUN apt-get update; apt-get -y full-upgrade                                                                                                                                                   
RUN apt-get -y install ca-certificates apt-transport-https wget gnupg                                                                                                                         
RUN wget -q https://packages.sury.org/php/apt.gpg -O- | apt-key add -                                                                                                                         
RUN echo "deb https://packages.sury.org/php/ stretch main" | tee /etc/apt/sources.list.d/php.list                                                                                             
RUN apt-get update                                                                                                                                                                            
RUN apt-get -y install apache2 php7.3 php7.3-cli php7.3-common php7.3-curl php7.3-mbstring php7.3-mysql php7.3-xml                                                                            
RUN a2enmod proxy proxy_http proxy_fcgi rewrite ssl                                                                                                                                           
COPY virtualhost.conf /etc/apache2/sites-available/000-default.conf
COPY virtualhost-ssl.conf /etc/apache2/sites-available/default-ssl.conf
RUN a2ensite default-ssl.conf
EXPOSE 80 443                                                                                                                                                                                 
CMD ["/usr/sbin/apache2ctl","-DFOREGROUND"]

