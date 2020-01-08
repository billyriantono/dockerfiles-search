############################################################
# Dockerfile to build a ELK stack server
# Based on darkside/centos65:base
############################################################

# Set the base image to Centos65 Base
FROM appcontainers/centos65

# File Author / Maintainer
MAINTAINER Rich Nason rnason@appcontainers.com

#*************************
#*       Versions        *
#*************************
ENV LSVER logstash-1.4.2
ENV ESVER elasticsearch-1.1.1
ENV KVER kibana-3.0.1


#**********************************
#* Override Enabled ENV Variables *
#**********************************
ENV FQDN kibana.local


#**************************
#*   Add Required Files   *
#**************************
ADD runconfig.sh /tmp/
ADD elasticsearch.repo /etc/yum.repos.d/

# Add GPG Keys for RPM installs
RUN rpm --import http://packages.elasticsearch.org/GPG-KEY-elasticsearch

# Download Kibana version specified in the Versions section.
RUN cd /tmp/ && \
wget https://download.elasticsearch.org/kibana/kibana/$KVER.tar.gz


#*************************
#*  Update and Pre-Reqs  *
#*************************
RUN yum clean all && \
yum -y update && \
yum -y install java-1.7.0-openjdk.x86_64 java-1.7.0-openjdk-devel.x86_64 nginx httpd-tools redis $ESVER $LSVER


#*************************
#*  Application Install  *
#*************************
# Unpack Kibana
RUN cd /tmp/ && \
mkdir -p /var/www/html/ && \
tar -xzvf kibana-3.0.1.tar.gz -C /var/www/html/

# Create some Symlink magic.
RUN cd /var/www/html/ && \
ln -s kibana-3.0.1 kibana3

# Add Dashboards
ADD /Dashboards/ /var/www/html/kibana3/app/dashboards/

# Redis
#*********
# Change redis listening address
RUN sed -ie 's/bind\ 127\.0\.0\.1/bind\ 0\.0\.0\.0/g' /etc/redis.conf


# ElasticSearch Config
#*********************


# Logstash Config
#****************
# Generate Certificate to allow log forwarders to use to send log data
RUN cd /etc/pki/tls && \
openssl req -x509 -batch -nodes -days 3650 -newkey rsa:2048 -keyout private/logstash-forwarder.key -out certs/logstash-forwarder.crt

# Add the preconstructed logstash configs to the logstash run directory
ADD /Configs/ /etc/logstash/conf.d/


# Kibana Config
#***************
# Copy the sample nginx config file from the kibana github
RUN cd /etc/nginx/conf.d/ && \
wget https://github.com/elasticsearch/kibana/raw/master/sample/nginx.conf


#************************
#* Post Deploy Clean Up *
#************************
RUN mkdir /tmp/installers && mv /tmp/*.tar.gz /tmp/installers/


#**************************
#*  Config Startup Items  *
#**************************
RUN chmod +x /tmp/runconfig.sh && \
echo "/tmp/./runconfig.sh" >> ~/.bashrc && \
echo "service redis start" >> ~/.bashrc && \
echo "service elasticsearch start" >> ~/.bashrc && \
echo "service logstash start" >> ~/.bashrc && \
echo "service nginx start" >> ~/.bashrc


#****************************
#* Expose Applicatoin Ports *
#****************************
# Expose ports to other containers only
EXPOSE 80
EXPOSE 443
EXPOSE 5000
EXPOSE 9200
EXPOSE 9300
