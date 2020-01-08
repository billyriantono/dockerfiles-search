FROM wordpress:latest
MAINTAINER The ZaneRay Group, support@zaneray.com

#update OS and add utilities
RUN apt-get update -y && apt-get install -y default-mysql-client wget

#add wp-cli
RUN cd ~ && wget https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar
RUN mv ~/wp-cli.phar /usr/local/bin/wp
RUN chmod 0744 /usr/local/bin/wp
RUN echo "alias wp='wp --allow-root'" >> ~/.bashrc

#add ssh keys so we can access test servers via SSH
# RUN mkdir -p /root/.ssh
# ADD /ssh/id_rsa /root/.ssh/id_rsa
# ADD /ssh/id_rsa.pub /root/.ssh/id_rsa.pub
# RUN chmod 0400 /root/.ssh/id_rsa
# RUN chmod 0600 /root/.ssh/id_rsa.pub

#add this so we can rsync later to the wordpress test server with a known_host
# RUN ssh-keyscan wordpress.test.zaneray.com >> /root/.ssh/known_hosts

#add ssl files
RUN mkdir -p /etc/ssl/certs
RUN mkdir -p /etc/ssl/private
ADD ./ssl/*.crt /etc/ssl/certs/
ADD ./ssl/*.key /etc/ssl/private/
RUN chmod -R 777 /etc/ssl

#add ssl vhost file
ADD ./httpd/zz_vhost.conf /etc/apache2/sites-enabled/

EXPOSE 80
EXPOSE 443

RUN mkdir -p /var/www/html/wp-content/uploads
RUN mkdir -p /var/www/html/wp-content/plugins

#install wordpress
#RUN wp core download --allow-root
#RUN ls -la /var/www/html
#RUN wp core install --url=proofresearch.zrdeskdev.com --title=Proof Research --admin_user=admin --admin_password=password --admin_email=support@zaneray.com 
#RUN wp core config --allow-root --dbhost=LOCALHOST --dbname=wordpress --dbuser=wordpress --dbpass=wordpress && chmod 644 wp-config.php
