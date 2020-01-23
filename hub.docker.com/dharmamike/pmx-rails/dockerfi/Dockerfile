FROM phusion/baseimage:0.9.12

MAINTAINER David Fry "dfry@drapoc.com"

# Set correct environment variables.
ENV HOME /root

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# Download and install Railo with Tomcat and Java

RUN curl http://www.getrailo.org/railo/remote/download42/4.2.1.000/tomcat/linux/railo-4.2.1.000-pl2-linux-x64-installer.run -o /root/railo-installer
RUN chmod u+x /root/railo-installer
RUN echo "startatboot=false" > /root/railo-options.txt
RUN echo "installconn=false" >> /root/railo-options.txt
RUN /root/railo-installer --mode unattended --railopass docker --optionfile /root/railo-options.txt

# Add startup scripts

ADD setenv.sh /opt/railo/tomcat/bin/
RUN chmod 755 /opt/railo/tomcat/bin/setenv.sh
RUN mkdir -p /etc/service/railo
ADD run.sh /opt/railo/run
RUN chmod 755 /opt/railo/run

# Post-install cleanup
RUN rm /root/railo-installer /root/railo-options.txt


# Public connector ports (8888 = HTTP 1.1, 8009 = AJP 1.3)
EXPOSE 8888 8009
