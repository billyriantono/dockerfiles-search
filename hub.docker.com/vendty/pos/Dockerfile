# Build with:
# 	docker build -t vendty/pos .

FROM ubuntu:16.04

ENV TERM=xterm

# Install curl, wget and net-stats for download the stack
RUN apt-get update && \
 apt install -yq curl net-tools psmisc wget

# Download the installer (5.5.39)
RUN XAMPP_DL_LINK=' \
	https://sourceforge.net/projects/xampp/files/XAMPP%20Linux/1.8.3/xampp-linux-x64-1.8.3-2-installer.run/download \
	' \ 
	&& wget $XAMPP_DL_LINK

# Run the installer in Unattended mode
# Currently there is a bug which doesnt show progress
RUN mv download xampp-linux-installer.run && chmod 755 xampp-linux-installer.run
RUN ./xampp-linux-installer.run --mode unattended --unattendedmodeui  minimal 

# Delete the installer file after install
RUN rm ./xampp-linux-installer.run

# Enable Apache web interface(remove security checks)
RUN /opt/lampp/bin/perl -pi -e s'/Require local/Require all granted/g' /opt/lampp/etc/extra/httpd-xampp.conf

# Enable includes of several configuration files
RUN mkdir /opt/lampp/apache2/conf.d && \
echo "IncludeOptional /opt/lampp/apache2/conf.d/*.conf" >> /opt/lampp/etc/httpd.conf

# Link to /usr/bin for easier starting
RUN ln -sf /opt/lampp/lampp /usr/bin/lampp

# Add xampp binaires to .bashrc
RUN echo "export PATH=\$PATH:/opt/lampp/bin/" >> /root/.bashrc
RUN echo "export TERM=xterm" >> /root/.bashrc

# Add .crt for curl requests
RUN wget -q https://curl.haxx.se/ca/cacert.pem -O /opt/lampp/share/curl/curl-ca-bundle.crt

# Add svg support
RUN echo "AddType image/svg+xml svg svgz" >> /opt/lampp/etc/httpd.conf
RUN echo "image/svg+xml svg svgz" >> /etc/mime.type

# Run Apache with user and group 'www-data'
RUN sed -i 's/User daemon/User www-data/' /opt/lampp/etc/httpd.conf
RUN sed -i 's/Group daemon/Group www-data/' /opt/lampp/etc/httpd.conf

# Add more ram and time execution
RUN echo "memory_limit=512M" >> /opt/lampp/etc/php.ini
RUN echo "max_execution_time=60" >> /opt/lampp/etc/php.ini


EXPOSE 80 443

ADD init.sh /usr/local/bin/init.sh
RUN chmod 777 /usr/local/bin/init.sh

# Start the init script
ENTRYPOINT ["/usr/local/bin/init.sh"]
