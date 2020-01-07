FROM centos:6

# Install Apache
RUN yum install httpd mod_ssl -y -q

# Script file for running apache in foreground
COPY httpd-foreground /usr/local/bin/
COPY ./httpd.conf /etc/httpd/conf/httpd.conf

# Get Webagent
RUN curl ftp://ftp.emc.com/pub/agents/Webagent/WebAgent_713_x64_All_Apache_128_01201414.zip -o /tmp/WebAgent.zip
WORKDIR /tmp
RUN yum install unzip tar rpcbind -q -y
#RUN echo 5d12009fc7bd290e8a4a50d533f6f885fbd0fa45 WebAgent.zip > WebAgent.zip.sha1
#RUN cat  WebAgent.zip.sha1
#RUN sha1sum -c WebAgent.zip.sha1
RUN unzip WebAgent.zip
RUN unzip WebAgent_71_Apache22_RHEL5_64_128_01201414.zip
RUN tar -C /etc/httpd/ -xvf /tmp/CD/rhel-5.1-x86-64/rsawebagent.tar
RUN rm -rf /tmp/Web* CD

# Symlink httpd.conf
RUN ln -s /etc/httpd/conf/httpd.conf /etc/httpd/rsawebagent/httpd.conf

#RUN echo include /etc/httpd/rsawebagent/rsawebagent.conf >> /etc/httpd/conf/httpd.conf
COPY RSAWebAgent.INI /etc/httpd/rsawebagent/RSAWebAgent.INI
COPY rsawebagent.conf /etc/httpd/conf.d/rsawebagent.conf

# /var/ace is where the secrets are stored
RUN mkdir -p /var/ace
VOLUME /var/ace
RUN chown -R apache /var/ace
# TODO: Not needed?
ENV VAR_ACE=/var/ace

# Make Apache own it
RUN chown -R apache /etc/httpd/rsawebagent

RUN ln -s /etc/httpd/rsawebagent/libaceclnt.so /usr/lib64/libaceclnt.so

EXPOSE 80
CMD ["httpd-foreground"]
