FROM        ubuntu:16.04
MAINTAINER  Gary Leong
 
ENV DEBIAN_FRONTEND noninteractive

# Update the package repository
RUN apt-get -qq update

# Install base system
RUN apt-get install -y varnish 

# Make our custom VCLs available on the container
#ADD default.vcl /etc/varnish/default.vcl

# Export environment variables
ENV VARNISH_PORT 80

# Expose port 80
EXPOSE 80

#ADD parse /parse
#ADD start /start
#RUN chmod 0755 /start /parse
#CMD ["/start"]

ADD run.sh /run.sh

CMD ["/run.sh"]

