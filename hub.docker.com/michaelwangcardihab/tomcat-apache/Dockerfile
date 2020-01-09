FROM tomcat:7-jre8

LABEL version="1.0.0"
LABEL maintainer="michael.wang@cardihab.com"

###########################
# Install Apache HTTP and mod jk
###########################
RUN apt-get update && \
    apt-get install -yq \
        apache2 \
        libapache2-mod-jk && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
RUN a2enmod ssl
RUN a2enmod rewrite

EXPOSE 80
EXPOSE 443

###########################
# Remove sample apps
###########################
RUN rm -rf /usr/local/tomcat/webapps/ROOT
RUN rm -rf /usr/local/tomcat/webapps/docs
RUN rm -rf /usr/local/tomcat/webapps/examples
RUN rm -rf /usr/local/tomcat/webapps/host-manager
RUN rm -rf /usr/local/tomcat/webapps/manager

###########################P
# Modify the jk workers config
###########################
RUN sed -i "s/workers.tomcat_home.*/workers.tomcat_home=\/usr\/local\/tomcat/g" /etc/libapache2-mod-jk/workers.properties
RUN sed -i "s/workers.java_home.*/workers.java_home=\/usr\/lib\/jvm\/java-8-openjdk-amd64/g" /etc/libapache2-mod-jk/workers.properties

###########################
# Modify the apache2 config
###########################
RUN truncate --size 0 /etc/apache2/sites-available/default-ssl.conf
RUN echo "\
<IfModule mod_ssl.c>\n\
\t<VirtualHost _default_:443>\n\
\t\tJkMount /* ajp13_worker\n\
\n\
\t\tServerAdmin \${APACHE_SERVER_ADMIN}\n\
\n\
\t\tDocumentRoot /usr/local/tomcat/webapps\n\
\n\
\t\tErrorLog \${APACHE_LOG_DIR}/error.log\n\
\t\tCustomLog \${APACHE_LOG_DIR}/access.log combined\n\
\n\
\t\tSSLEngine on\
\n\
\t\tSSLCertificateFile /etc/apache2/ssl.crt/server-certificate.crt\n\
\t\tSSLCertificateKeyFile /etc/apache2/ssl.crt/server-certificate.key\n\
\t\tSSLCertificateChainFile /etc/apache2/ssl.crt/server-chain-certificate.crt\n\
\n\
\t</VirtualHost>\n\
</IfModule>\
" > /etc/apache2/sites-available/default-ssl.conf
RUN truncate --size 0 /etc/apache2/sites-available/000-default.conf
RUN echo "\
<VirtualHost *:80>\n\
\tRewriteEngine On\n\
\tRewriteCond %{HTTPS} !=on\n\
\tRewriteRule ^/?(.*) https://%{SERVER_NAME}/\$1 [R,L]\n\
</VirtualHost>\
" > /etc/apache2/sites-available/000-default.conf
RUN echo "ServerName \${APACHE_SERVER_NAME}" > /etc/apache2/conf-available/servername.conf
RUN ln -s /etc/apache2/conf-available/servername.conf /etc/apache2/conf-enabled/servername.conf
RUN ln -s /etc/apache2/sites-available/default-ssl.conf /etc/apache2/sites-enabled/default-ssl.conf

###########################
# Add run Scripts
###########################
ADD run.sh /run.sh
RUN chmod +x /*.sh

CMD ["/run.sh"]
