FROM x110dc/rundeck

MAINTAINER B Waller bjorn@waller.nu

# Download Rundeck
ADD http://download.rundeck.org/deb/rundeck-2.5.0-1-GA.deb /tmp/rundeck.deb

# Run the installation script
RUN /install.sh

ADD profile /etc/rundeck/profile

# Add winrm plugin 
ADD https://github.com/rundeck-plugins/rundeck-winrm-plugin/releases/download/v1.2/rundeck-winrm-plugin-1.2.jar  /var/lib/rundeck/libext/rundeck-winrm-plugin-1.2.jar

RUN chmod 644 /var/lib/rundeck/libext/rundeck-winrm-plugin-1.2.jar
