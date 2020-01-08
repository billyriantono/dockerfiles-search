From ubuntu
RUN apt-get -y update
RUN apt-get -y install apache2 libapache2-mod-php7.0 php7.0 git
RUN git clone https://github.com/TomZastrow/reptor.git /var/www/html/reptor
CMD service apache2 start  && tail -F /var/log/messages
