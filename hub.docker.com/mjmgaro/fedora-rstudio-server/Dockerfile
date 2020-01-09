FROM mjmg/fedora-r-base:latest

RUN \
  wget https://s3.amazonaws.com/rstudio-dailybuilds/rstudio-server-rhel-1.0.44-x86_64.rpm && \
  dnf install -y --nogpgcheck rstudio-server-rhel-1.0.44-x86_64.rpm && \
  rm rstudio-server-rhel-1.0.44-x86_64.rpm

RUN \
  useradd rstudio && \
  echo "rstudio:rstudio" | chpasswd
  
# Rstudio ports
EXPOSE 8004

COPY \
  add-students.sh /usr/local/bin/add-students.sh
  
RUN \
  chmod u+x /usr/local/bin/add-students.sh && \
  /usr/local/bin/add-students.sh

#COPY \
#  rstudio-server.conf /etc/supervisor/conf.d/rstudio-server.conf
  
# default command
#CMD ["supervisord", "-c", "/etc/supervisor.conf"]
CMD ["/usr/lib/rstudio-server/bin/rserver"]
