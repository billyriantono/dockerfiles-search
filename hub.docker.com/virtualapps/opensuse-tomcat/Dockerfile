FROM opensuse:latest
MAINTAINER "Virtual Apps <tovirtualapps@gmail.com>"
LABEL description="use this image to host your JAVA Servlets"

# install tomcat using zypper
RUN zypper -n update && zypper -n install tomcat 

# tomcat web service related files
RUN  mkdir -p /usr/share/tomcat/webapps/ROOT
RUN  chown -R tomcat:tomcat /usr/share/tomcat/

# Setting up tomcat environment variables
RUN su - tomcat
ENV CATALINA_BASE=/usr/share/tomcat/
ENV CATALINA_HOME=/usr/share/tomcat/
ENV CATALINA_TMPDIR=/var/cache/tomcat/temp/

# create welcome file
RUN chmod -R 755 /usr/share/tomcat/webapps
RUN echo "Welcome to virtualapps/opensuse-tomcat, copy your warfile to /usr/share/tomcat/webapps/" > /usr/share/tomcat/webapps/ROOT/index.html 

## Setup TLS
#  Generate key
RUN keytool -genkey \
    -keyalg RSA \
    -keystore /usr/share/tomcat/.keystore \
    -dname "cn=VirtualApps-OpenSuse-Tomcat, ou=IT, o=VirtualApps, c=IN" \
    -storepass password -keypass password

# Setup TLS configuration in Tomcat server configuration file
RUN sed -i "s#</Server>##g" /usr/share/tomcat/conf/server.xml; \
	sed -i "s#  </Service>##g" /usr/share/tomcat/conf/server.xml; \
	echo '    <Connector port="8443" protocol="HTTP/1.1" SSLEnabled="true" maxThreads="150" scheme="https" secure="true" clientAuth="false" sslProtocol="TLS" keystoreFile="/usr/share/tomcat/.keystore" keystorePass="password" />' >> /usr/share/tomcat/conf/server.xml; \
	echo '  </Service>' >> /usr/share/tomcat/conf/server.xml; \
	echo '</Server>' >> /usr/share/tomcat/conf/server.xml

# Setting working directory for web service
WORKDIR /usr/share/tomcat

# Container should run as tomcat user by default and not root
USER tomcat

# Making the container executable so that user just needs to do
# docker run -d -p [host-port]:[container-port] [container-image]
# docker run -d -p 80:8080 -p 443:8443 virtualapps/opensuse-tomcat
ENTRYPOINT /usr/sbin/tomcat-sysd start

