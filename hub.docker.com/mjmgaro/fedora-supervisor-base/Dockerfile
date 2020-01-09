FROM fedora:latest

# Update System Image
RUN \
  dnf update -y && \
  dnf upgrade -y
  
#install additional tools 
RUN \
  dnf install -y unzip wget
  
# Configure Supervisor
RUN \
  dnf install -y python-setuptools && \
  easy_install supervisor && \
  mkdir -p /var/log/supervisor
  
# supervisor base configuration
ADD supervisord.conf /etc/supervisor/supervisord.conf

# default command
#CMD ["supervisord", "-c", "/etc/supervisor.conf"]
CMD ["/bin/bash"]
