# Pull base image.
FROM centos 

#Create directory /var/www/html for nginx, because the image i will use to create nginx container use /var/www/html as it's work directory (DocumentRoot).
RUN mkdir -p /var/www/html 

#Create documentroot directory for mariadb.
RUN mkdir -p /var/lib/mysql

#Creating user and group nginx with uid and guid.
RUN groupadd -g 115 nginx
RUN useradd -u 115 -g 115 nginx
 
#Declare the work directory
WORKDIR ["/var/www/html"]

# Install wget
RUN yum install wget -y && \

#Enter in the directory /var/www/html.
cd /var/www/html && \

#Installation of latest version of wordpress.
wget https://wordpress.org/latest.tar.gz && \

#Extract the wordpress directory.
tar -xvf latest.tar.gz && \

# As we already extract the wordpress directory we delete the latest.tar.gz file.
rm -f latest.tar.gz && \

#Copy all the files from the directory /var/www/html/wordpress to //var/www/html//html.
mv  /var/www/html/wordpress/* /var/www/html && \

#Delete wordpress directory.
rm -rf wordpress/ && \

#Recursively change the owner of /var/www/html to nginx.
chown -R nginx:nginx /var/www/html && \

#Recursively change the permission of directory /var/www/html to 755.
chmod -R 755 /var/www/html

#Difine mountable directories.
VOLUME ["/var/www/html" , "/var/lib/mysql"]

