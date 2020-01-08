FROM ubuntu:14.04 
#Upgrade the current repo and system 
RUN apt-get update -y && apt-get upgrade -y
#Install base packages for the application 
#Disable interactive prompts during package installation 
ENV DEBIAN_FRONTEND noninteractive 
RUN sed -i 's/^mesg n$/tty -s \&\& mesg n/g' /root/.profile 
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y git curl apache2 php5 
#Apply 10 seconds delay to complete the package installation
RUN sleep 10 
#CMD ["/usr/bin/apt-get", "install", "-y", "libapache2-mod-php5 php5-mcrypt php5-mysql php5-gd php5-ldap"] #install necessary modules to work with the application 
RUN DEBIAN_FRONTEND=noninteractive /usr/bin/apt-get install -y libapache2-mod-php5 php5-mcrypt php5-mysql php5-gd php5-ldap 
RUN sleep 10 
#CMD ["/usr/bin/apt-get", "install", "-y", "php5-mysql php5-mssql php5-sybase php5-sqlite vsftpd"]
RUN DEBIAN_FRONTEND=noninteractive /usr/bin/apt-get install -y php5-mysql php5-mssql php5-sybase php5-sqlite vsftpd 
RUN sleep 10
#Install NFS package to mount EFS 
RUN apt-get install -y nfs-common 
#RUN rm -rf /var/www/* #Create a directory to mount EFS 
#RUN mkdir /storage 
#Mount EFS to /storage directory 
#RUN /bin/mount -t nfs4 $(curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone).fs-078a66ae.efs.us-west-2.amazonaws.com:/ /storage
#Enable rewrite module RUN a2enmod rewrite
#Set User,Group and Log for apache 
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data 
ENV APACHE_LOG_DIR /var/log/apache2 
ENV ALLOW_OVERRIDE **False** 
#Change the document root to the desired location 
#RUN sed -i "s_/var/www/html/_/storage/var/www/html_" /etc/apache2/sites-available/application.conf 
#Activate the application #RUN a2ensite application 
#Restart apache RUN service apache2 restart 
#Provide user and group permission for the document root 
#RUN /bin/chown -R www-data:www-data /storage/var/www/ 
#Open the apache port 80 
EXPOSE 80 
RUN service apache2 start
RUN apt-get install sysv-rc-conf -y
 #Enable apache service to start evenafter reboot
CMD ["/usr/sbin/sysv-rc-conf", "apache2", "on"]
